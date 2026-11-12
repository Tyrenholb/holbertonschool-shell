# Shell - Holberton School

This repository contains my shell projects from Holberton School. The exercises
cover navigating the filesystem, managing files, working with variables and
expansions, filtering text, and understanding Linux permissions and ownership.

There are 73 short Bash scripts across four project folders. Each folder has
a README explaining every script, its inputs, and how to use it.

## Project folders

| Folder | Scripts | What it covers |
| --- | --- | --- |
| [`basics`](basics/README.md) | 18 | Working directories, file listings, directory creation, copying, moving, deletion, symbolic links, and filename patterns |
| [`init_files_variables_and_expansions`](init_files_variables_and_expansions/README.md) | 15 | Aliases, shell and environment variables, PATH, arithmetic, base conversion, brace expansion, and formatted numbers |
| [`io_redirections_and_filters`](io_redirections_and_filters/README.md) | 23 | Pipes, redirection, file contents, line selection, sorting, unique lines, searches, character transformations, and directory traversal |
| [`permissions`](permissions/README.md) | 17 | User identity, group membership, symbolic and numeric modes, ownership changes, and symbolic-link ownership |

## Requirements

- Bash. Each numbered script begins with `#!/bin/bash`.
- A Linux environment with standard GNU utilities and tools such as `file`
  and `rev` for the tasks that use them.
- Any task-specific files, environment variables, users, groups, and access
  permissions described in the folder README.

These are shell scripts, so there is no C compilation step or Betty check.
The tasks are independent exercises rather than one application with a shared
build or startup command.

## How to use the scripts

From the repository root, enter a project folder and choose a script:

```bash
cd basics
bash 0-current_working_directory
bash 1-listit
```

The first prints the current directory; the second lists its visible entries.
Running a script with `bash` does not require its executable permission bit.

Commands using relative paths act on the directory you run them from. They do
not automatically switch to the directory containing the script.

### Variables and standard input

Some tasks take input through environment variables:

```console
$ BINARY=1010 bash init_files_variables_and_expansions/11-binary_to_decimal
10
```

Others read standard input through a pipe:

```console
$ printf 'hello\n' | bash io_redirections_and_filters/21-reverse
olleh
```

Run those two examples from the repository root.

### Scripts that change shell state

A script run with `bash` executes in a child shell. Its directory changes,
variables, and aliases do not persist in the calling shell. For example, to
change your current directory using the home-directory exercise, run from the
repository root:

```bash
source basics/2-bring_me_home
```

Source only a script whose commands you have inspected. In particular,
`init_files_variables_and_expansions/0-alias` defines `ls` as `rm -f *`.
It is a destructive alias exercise and should not be sourced into your normal
working session.

## Syntax checks

From the repository root, parse every exercise without executing it:

```bash
for folder in basics init_files_variables_and_expansions io_redirections_and_filters permissions; do
    for script in "$folder"/[0-9]*; do
        bash -n "$script"
    done
done
```

All 73 scripts passed local Bash syntax checks. Selected output examples and
file operations were also verified, using temporary storage for file changes.
Account switching and ownership changes were not executed against the host's
users or project files. Syntax checks do not verify runtime prerequisites or
all behavior.

## Working with task files

Read the selected script and its folder README before running it. Some scripts
use fixed paths under `/tmp` or read `/etc` files. Others overwrite files,
append content, move matching entries, delete files recursively, or change
permissions and ownership.

Use disposable exercise files for those tasks. Scripts that name users or
groups expect them to exist already, and some operations require additional
privileges. There is no need to run every script in sequence to explore the
repository.
