# etckeeper Cheat Sheet

`etckeeper` stores `/etc` in version control, usually Git, so configuration changes can be reviewed, committed, and reverted.

It integrates with package managers such as `apt` and can automatically commit changes made to `/etc` during package installation and upgrades.

> Security note: `/etc` may contain sensitive files such as `/etc/shadow`. Keep the entire repository, including `/etc/.git`, private and protected.

## Install

On Ubuntu/Debian:

```bash
sudo apt update
sudo apt install etckeeper
```

In many packaged installations, initialization is performed automatically during installation.

Check:

```bash
sudo etckeeper vcs status
```

## Initialize `/etc`

If needed:

```bash
sudo etckeeper init
```

This initializes a version-control repository in `/etc` (Git by default) and stages relevant files.

Create the initial commit:

```bash
sudo etckeeper commit "Initial /etc commit"
```

## Check repository status

Using etckeeper:

```bash
sudo etckeeper vcs status
```

Or directly with Git:

```bash
cd /etc
sudo git status
```

## View changes

```bash
cd /etc
sudo git diff
```

View staged changes:

```bash
sudo git diff --cached
```

## Commit configuration changes

```bash
sudo etckeeper commit "Describe the configuration change"
```

Example:

```bash
sudo etckeeper commit "Update SSH server configuration"
```

You can also use normal Git commands inside `/etc`:

```bash
cd /etc
sudo git add ssh/sshd_config
sudo git commit -m "Update SSH server configuration"
```

## View history

```bash
cd /etc
sudo git log --oneline
```

Show changes in a commit:

```bash
sudo git show <commit>
```

History for one file:

```bash
sudo git log -- /etc/ssh/sshd_config
```

## Compare file versions

```bash
cd /etc
sudo git diff HEAD~1 -- ssh/sshd_config
```

Compare two commits:

```bash
sudo git diff <commit1> <commit2> -- ssh/sshd_config
```

## Restore a file

Restore a file to the last committed version:

```bash
cd /etc
sudo git restore ssh/sshd_config
```

Restore from a specific commit:

```bash
sudo git restore --source=<commit> ssh/sshd_config
```

For older Git versions:

```bash
sudo git checkout <commit> -- ssh/sshd_config
```

## Package-manager integration

With `apt`, etckeeper normally runs hooks before and after package operations.

Typical workflow:

```text
apt starts
   ↓
etckeeper pre-install
   ↓
packages modify /etc
   ↓
etckeeper post-install
   ↓
changes are committed
```

This means commands such as:

```bash
sudo apt install <package>
sudo apt upgrade
```

may automatically produce etckeeper commits when `/etc` changes.

## Main configuration file

```text
/etc/etckeeper/etckeeper.conf
```

View it:

```bash
sudo less /etc/etckeeper/etckeeper.conf
```

Common settings include the VCS backend and package-manager integration.

## Hook directories

etckeeper is modular and executes scripts from directories under:

```text
/etc/etckeeper/
```

Common hook directories include:

```text
/etc/etckeeper/pre-install.d/
/etc/etckeeper/post-install.d/
/etc/etckeeper/pre-commit.d/
/etc/etckeeper/commit.d/
/etc/etckeeper/update-ignore.d/
```

## Update `.gitignore`

Regenerate/update etckeeper-managed ignore rules:

```bash
sudo etckeeper update-ignore
```

Inspect:

```bash
sudo less /etc/.gitignore
```

## File metadata

Git does not normally preserve all Unix metadata needed for `/etc`, such as ownership and full permissions.

etckeeper stores additional metadata in:

```text
/etc/.etckeeper
```

This helps preserve information such as file ownership, permissions, and empty directories.

## Run Git commands through etckeeper

The `vcs` command passes arguments to the configured VCS:

```bash
sudo etckeeper vcs status
sudo etckeeper vcs log --oneline
sudo etckeeper vcs diff
```

This is useful when you do not want to `cd /etc` first.

## Uninitialize etckeeper

```bash
sudo etckeeper uninit
```

> Warning: with Git, this removes the `/etc/.git` repository. Do not run this unless you intentionally want to remove etckeeper version history.

## Backup / remote repository

Because `/etc` may contain secrets, do **not** push the repository to a public Git repository.

If you use a remote backup, it must be private and access-controlled.

Add a remote:

```bash
cd /etc
sudo git remote add backup <private-repository-url>
```

Push:

```bash
sudo git push backup <branch>
```

Check remotes:

```bash
sudo git remote -v
```

## Useful examples

See what changed recently:

```bash
cd /etc
sudo git status
sudo git diff
```

Commit a manual configuration change:

```bash
sudo etckeeper commit "Adjust nginx configuration"
```

Inspect package-generated changes:

```bash
cd /etc
sudo git log --oneline -10
sudo git show HEAD
```

Find who changed a line:

```bash
cd /etc
sudo git blame ssh/sshd_config
```

## Quick reference

```bash
sudo apt install etckeeper                    # Install
sudo etckeeper init                           # Initialize /etc repository
sudo etckeeper commit "message"               # Commit /etc changes
sudo etckeeper vcs status                     # Show status
sudo etckeeper vcs diff                       # Show changes
sudo etckeeper vcs log --oneline              # Show history
sudo etckeeper update-ignore                  # Update ignore rules
sudo etckeeper uninit                         # Remove VCS repository

cd /etc
sudo git status
sudo git diff
sudo git log --oneline
sudo git show <commit>
sudo git restore <file>
```

## Minimal workflow

```bash
sudo etckeeper vcs status
sudo etckeeper vcs diff
sudo etckeeper commit "Describe the change"
```
