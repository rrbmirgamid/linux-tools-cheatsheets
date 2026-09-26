# Ubuntu Server Baseline

A practical baseline of tools I commonly install on a fresh Ubuntu Server.

This is not intended to be a minimal package set. It is a personal admin toolbox for interactive shell use, troubleshooting, configuration tracking, file management, and general server maintenance.

## Core baseline

```bash
sudo apt update

sudo apt install   etckeeper   pydf   colordiff   btm   bat   mc   screen   trash-cli   git
```

## Recommended additions

These are also commonly useful on fresh servers:

```bash
sudo apt install   curl   wget   jq   rsync   unzip   zip   tree   ncdu   lsof   dnsutils   ca-certificates   gnupg
```

## Package overview

### Configuration tracking

#### etckeeper

Tracks `/etc` in version control, usually Git.

```bash
sudo apt install etckeeper
```

Useful for reviewing configuration changes and tracking modifications made by package upgrades.

---

### Filesystem and disk usage

#### pydf

A more readable alternative to `df`.

```bash
sudo apt install pydf
```

#### ncdu

Interactive disk usage browser.

```bash
sudo apt install ncdu
```

#### tree

Displays directory structures as a tree.

```bash
sudo apt install tree
```

---

### Process and system monitoring

#### btm

`bottom` (`btm`) is an interactive system monitor.

```bash
sudo apt install btm
```

Useful for CPU, memory, disk, process, and network monitoring.

---

### File viewing and diff tools

#### bat

A modern `cat` replacement with syntax highlighting, line numbers, Git integration, and paging.

```bash
sudo apt install bat
```

On some Ubuntu/Debian versions, the executable may be named `batcat`.

#### colordiff

Adds color to standard `diff` output.

```bash
sudo apt install colordiff
```

---

### File management

#### mc

Midnight Commander, a terminal-based file manager.

```bash
sudo apt install mc
```

#### trash-cli

Command-line Trash implementation.

```bash
sudo apt install trash-cli
```

Useful commands:

```bash
trash-put <file-or-directory>
trash-list
trash-restore
trash-rm '/full/original/path'
trash-empty
```

---

### Terminal sessions

#### screen

Persistent terminal sessions.

```bash
sudo apt install screen
```

Alternative:

```bash
sudo apt install tmux
```

I usually install one of these depending on the environment.

---

### Version control

#### git

```bash
sudo apt install git
```

Git is often already installed, but I still treat it as part of the baseline.

Check:

```bash
git --version
```

---

### Network and HTTP tools

#### curl

```bash
sudo apt install curl
```

Useful for HTTP requests, APIs, downloading files, and metadata endpoints.

#### wget

```bash
sudo apt install wget
```

Useful for non-interactive file downloads.

#### dnsutils

```bash
sudo apt install dnsutils
```

Provides tools such as:

```bash
dig
nslookup
```

#### lsof

```bash
sudo apt install lsof
```

Useful for finding open files and identifying which process is using a port.

Example:

```bash
sudo lsof -i :443
```

---

### Data processing

#### jq

Command-line JSON processor.

```bash
sudo apt install jq
```

Example:

```bash
curl -s https://example.com/api | jq
```

---

### Archive tools

#### unzip / zip

```bash
sudo apt install unzip zip
```

---

### File synchronization

#### rsync

```bash
sudo apt install rsync
```

Useful for local and remote file synchronization and backups.

---

### Repository and TLS support

#### ca-certificates

```bash
sudo apt install ca-certificates
```

Provides trusted CA certificates for TLS connections.

#### gnupg

```bash
sudo apt install gnupg
```

Useful for repository signing keys and GPG operations.

---

## One-command install

Core baseline plus recommended utilities:

```bash
sudo apt update && sudo apt install -y   etckeeper   pydf   colordiff   btm   bat   mc   screen   trash-cli   git   curl   wget   jq   rsync   unzip   zip   tree   ncdu   lsof   dnsutils   ca-certificates   gnupg
```

## Optional tools

Depending on the server role, I may also install:

```text
tmux        Alternative to screen
vim         Editor
nano        Simple editor
htop        Process monitor
ripgrep     Fast recursive text search
fd-find     Fast alternative to find
fzf         Fuzzy finder
shellcheck  Shell script analysis
```

Install as needed:

```bash
sudo apt install tmux vim nano htop ripgrep fd-find fzf shellcheck
```

## Suggested repository layout

```text
linux-tools-cheatsheets/
├── ubuntu-server-baseline/
│   └── README.md
├── bat/
│   └── README.md
├── btm/
│   └── README.md
├── etckeeper/
│   └── README.md
├── ffmpeg/
│   └── README.md
├── trash-cli/
│   └── README.md
└── yt-dlp/
    └── README.md
```

## Quick checklist

```text
[ ] etckeeper
[ ] pydf
[ ] colordiff
[ ] btm
[ ] bat
[ ] mc
[ ] screen
[ ] trash-cli
[ ] git
[ ] curl
[ ] wget
[ ] jq
[ ] rsync
[ ] unzip / zip
[ ] tree
[ ] ncdu
[ ] lsof
[ ] dnsutils
[ ] ca-certificates
[ ] gnupg
```
