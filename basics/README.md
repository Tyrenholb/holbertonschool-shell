# Shell Basics

Eighteen short Bash scripts practise moving around the filesystem, listing
files, creating directories, and working with files and symbolic links.
Each script focuses on one command.

## Scripts

| Script | What it does |
| --- | --- |
| [`0-current_working_directory`](0-current_working_directory) | Prints the current working directory with `pwd` |
| [`1-listit`](1-listit) | Lists visible entries in the current directory |
| [`2-bring_me_home`](2-bring_me_home) | Changes to the current user's home directory |
| [`3-listfiles`](3-listfiles) | Lists entries in long format |
| [`4-listmorefiles`](4-listmorefiles) | Lists entries, including hidden ones, in long format |
| [`5-listfilesdigitonly`](5-listfilesdigitonly) | Uses long format with hidden entries and numeric owner/group IDs |
| [`6-firstdirectory`](6-firstdirectory) | Creates `/tmp/my_first_directory` |
| [`7-movethatfile`](7-movethatfile) | Moves `/tmp/betty` into `/tmp/my_first_directory` |
| [`8-firstdelete`](8-firstdelete) | Removes `/tmp/my_first_directory/betty` |
| [`9-firstdirdeletion`](9-firstdirdeletion) | Removes `/tmp/my_first_directory` if it is empty |
| [`10-back`](10-back) | Changes to the previous working directory with `cd -` |
| [`11-lists`](11-lists) | Lists the current directory, its parent, and `/boot` in long format, including hidden entries |
| [`12-file_type`](12-file_type) | Reports the type of `/tmp/iamafile` |
| [`13-symbolic_link`](13-symbolic_link) | Creates `__ls__` pointing to `/bin/ls` in the current directory |
| [`14-copy_html`](14-copy_html) | Copies matching `.html` files to the parent directory when missing there or newer than the destination |
| [`15-lets_move`](15-lets_move) | Moves entries matching `[A-Z]*` to `/tmp/u` |
| [`16-clean_emacs`](16-clean_emacs) | Removes entries matching `*~` using `rm` |
| [`17-tree`](17-tree) | Creates the nested path `welcome/to/school` |

## Requirements

- Bash, using the `#!/bin/bash` interpreter line in each script.
- A Linux environment with GNU core utilities and the `file` command.
- The files, directories, and access permissions needed by the selected task.

These are shell exercises; GCC and Betty C checks do not apply.

## Syntax checks

From the repository root:

```bash
cd basics
for script in [0-9]*; do
    bash -n "$script"
done
```

All 18 scripts pass Bash syntax checks locally. A syntax check parses a script
without running its commands; it does not check whether task files exist.

## Usage

Run a script from this directory with Bash:

```bash
bash 0-current_working_directory
bash 1-listit
```

The commands operate on your current working directory, not automatically on
the script's directory. For directory changes that should affect your current
shell, source the relevant script:

```bash
source ./2-bring_me_home
```

To return to the previous location, use the path to `10-back` or return to this
folder before sourcing it. `cd -` needs a previous directory in `OLDPWD`.
Running a `cd` script with `bash` changes only the child shell's directory.

## Task setup and file changes

- Tasks `6` through `9` form a create/move/delete sequence. They expect a
  disposable `/tmp/betty` file and use fixed paths, so check those paths before
  running them.
- `12-file_type` expects `/tmp/iamafile`. `15-lets_move` expects `/tmp/u` to
  exist as a directory for moving multiple entries.
- `13-symbolic_link` requires that `__ls__` does not already exist.
- Copy, move, and delete scripts act on matching entries. In particular,
  `16-clean_emacs` deletes matching backup files rather than listing them.
- Unmatched patterns, missing files, existing directories, or insufficient
  permissions can make these minimal commands fail. The scripts do not add
  custom error handling.
