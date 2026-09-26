# bat Cheat Sheet

`bat` is a modern `cat` replacement with syntax highlighting, line numbers, Git integration, and paging.

## Install

On Ubuntu/Debian:

```bash
sudo apt install bat
```

Depending on the distribution/version, the executable may be available as `bat` or `batcat`.

Check:

```bash
bat --version
batcat --version
```

## Basic usage

Display a file:

```bash
bat file.txt
```

Display multiple files:

```bash
bat file1.txt file2.txt
```

Display matching files:

```bash
bat *.conf
```

## Show line numbers

```bash
bat -n file.txt
```

## Plain output

Disable decorations such as line numbers and Git markers:

```bash
bat -p file.txt
```

Equivalent long option:

```bash
bat --plain file.txt
```

## Show non-printable characters

```bash
bat -A file.txt
```

## Force syntax highlighting language

```bash
bat -l json file.txt
bat -l yaml file.txt
bat -l bash script
```

## Read from stdin

```bash
command | bat
```

Example:

```bash
cat file.json | bat -l json
```

## Display only a line range

```bash
bat --line-range 10:30 file.txt
```

From line 100 onward:

```bash
bat --line-range 100: file.txt
```

## Disable paging

```bash
bat --paging=never file.txt
```

## Force paging

```bash
bat --paging=always file.txt
```

## If your system uses `batcat`

Create an alias:

```bash
alias bat='batcat'
```

To make it permanent in Bash:

```bash
echo "alias bat='batcat'" >> ~/.bashrc
source ~/.bashrc
```

Alternatively, create a symlink:

```bash
mkdir -p ~/.local/bin
ln -s /usr/bin/batcat ~/.local/bin/bat
```

## Useful examples

View a configuration file:

```bash
bat /etc/ssh/sshd_config
```

View JSON with explicit syntax highlighting:

```bash
bat -l json data.json
```

Pipe command output through `bat`:

```bash
curl -s https://example.com/file.json | bat -l json
```

Use with `find`:

```bash
find . -name '*.conf' -exec bat {} +
```

## Quick reference

```bash
bat file                     # Display file
bat -n file                  # Show line numbers
bat -p file                  # Plain output
bat -A file                  # Show non-printable characters
bat -l json file             # Force syntax
bat --line-range 10:30 file  # Show selected lines
bat --paging=never file      # Disable pager
command | bat                # Read from stdin
```
