# trash-cli Cheat Sheet

A short reference for using `trash-cli` on Linux.

## Install

```bash
sudo apt install trash-cli
```

## Move a file or directory to Trash

```bash
trash-put file_or_directory
```

Examples:

```bash
trash-put file.txt
trash-put my-directory
```

## List Trash contents

```bash
trash-list
```

## Restore an item

```bash
trash-restore
```

This opens an interactive prompt where you can select the item to restore.

## Permanently delete one item

Use the item's original full path:

```bash
trash-rm '/full/original/path'
```

Example:

```bash
trash-rm '/srv/tmp/project/test-directory'
```

Using the full path is safer when multiple deleted items have the same name.

## Empty the entire Trash

```bash
trash-empty
```

## Delete items older than N days

Example: delete items older than 30 days:

```bash
trash-empty 30
```

## Default Trash location

For the current user:

```text
~/.local/share/Trash/
```

Typical structure:

```text
~/.local/share/Trash/
├── files/   # Deleted files and directories
└── info/    # Original paths and deletion timestamps
```

## Quick reference

```bash
trash-put file_or_directory        # Move to Trash
trash-list                         # List Trash contents
trash-restore                      # Restore interactively
trash-rm '/full/original/path'     # Permanently delete one item
trash-empty                        # Empty the entire Trash
trash-empty 30                     # Delete items older than 30 days
```

> `trash-put` is generally safer for interactive shell use than `rm -rf`, because deleted items can be restored until they are permanently removed from the Trash.
