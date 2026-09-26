# delta Cheat Sheet

`delta` is a syntax-highlighting pager for Git, diff, grep, and blame output.

> Package name: usually `git-delta`  
> Executable: `delta`

## Install

On Ubuntu/Debian, if available in your configured repositories:

```bash
sudo apt install git-delta
```

Check the installed version:

```bash
delta --version
```

## Configure Git to use delta

Recommended global configuration:

```bash
git config --global core.pager delta
git config --global interactive.diffFilter 'delta --color-only'
git config --global delta.navigate true
git config --global merge.conflictStyle zdiff3
```

Optional: explicitly use dark mode:

```bash
git config --global delta.dark true
```

Or light mode:

```bash
git config --global delta.light true
```

If neither is set, delta can auto-detect the terminal background.

Equivalent `~/.gitconfig` configuration:

```ini
[core]
    pager = delta

[interactive]
    diffFilter = delta --color-only

[delta]
    navigate = true
    dark = true

[merge]
    conflictStyle = zdiff3
```

## Common Git commands

Once configured, delta is used automatically by commands such as:

```bash
git diff
git show
git log -p
git stash show -p
git reflog -p
git blame <file>
```

## Side-by-side view

Temporary:

```bash
git diff | delta --side-by-side
```

Enable globally:

```bash
git config --global delta.side-by-side true
```

Equivalent config:

```ini
[delta]
    side-by-side = true
```

## Line numbers

Temporary:

```bash
git diff | delta --line-numbers
```

Enable globally:

```bash
git config --global delta.line-numbers true
```

Equivalent config:

```ini
[delta]
    line-numbers = true
```

## Navigate between diff sections

Enable navigation:

```bash
git config --global delta.navigate true
```

Inside the pager:

```text
n    next diff section / file
N    previous diff section / file
```

## Use delta with normal diff output

```bash
diff -u old.txt new.txt | delta
```

## Show available syntax themes

Dark themes:

```bash
delta --show-syntax-themes --dark
```

Light themes:

```bash
delta --show-syntax-themes --light
```

Use a specific syntax theme:

```bash
delta --syntax-theme 'Dracula'
```

Configure globally:

```bash
git config --global delta.syntax-theme Dracula
```

## Show delta themes

```bash
delta --show-themes
```

## Temporary options

Use line numbers for one command:

```bash
git diff | delta --line-numbers
```

Use side-by-side mode for one command:

```bash
git diff | delta --side-by-side
```

Use both:

```bash
git diff | delta --side-by-side --line-numbers
```

## Disable delta temporarily

Bypass the configured pager:

```bash
git --no-pager diff
```

Or use Git's default pager for one command:

```bash
GIT_PAGER=less git diff
```

## Help

Short help:

```bash
delta -h
```

Full help:

```bash
delta --help
```

## Quick reference

```bash
delta --version                             # Show version
delta -h                                    # Short help
delta --help                                # Full help
delta --show-syntax-themes --dark           # List dark syntax themes
delta --show-syntax-themes --light          # List light syntax themes
delta --show-themes                         # Show delta themes

git config --global core.pager delta
git config --global interactive.diffFilter 'delta --color-only'
git config --global delta.navigate true
git config --global delta.side-by-side true
git config --global delta.line-numbers true
git config --global merge.conflictStyle zdiff3
```

## Minimal recommended configuration

```ini
[core]
    pager = delta

[interactive]
    diffFilter = delta --color-only

[delta]
    navigate = true

[merge]
    conflictStyle = zdiff3
```
