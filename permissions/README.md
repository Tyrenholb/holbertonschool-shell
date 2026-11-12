# Shell Permissions

Seventeen Bash scripts practise user identity, groups, ownership, and permission
bits. They use `su`, `whoami`, `groups`, `chmod`, `chown`, and `chgrp`, plus
simple file and directory creation commands.

## Scripts

| Script | What it does |
| --- | --- |
| [`0-iam_betty`](0-iam_betty) | Starts a shell as the user `betty` with `su` |
| [`1-who_am_i`](1-who_am_i) | Prints the current effective username |
| [`2-groups`](2-groups) | Lists the current user's group memberships |
| [`3-new_owner`](3-new_owner) | Changes the owner of `hello` to `betty` |
| [`4-empty`](4-empty) | Creates `hello` if absent, or updates its timestamps if present |
| [`5-execute`](5-execute) | Adds owner execute permission to `hello` |
| [`6-multiple_permissions`](6-multiple_permissions) | Adds owner/group execute and other-user read permission to `hello` |
| [`7-everybody`](7-everybody) | Adds execute permission for everyone on `hello` |
| [`8-James_Bond`](8-James_Bond) | Sets `hello` to mode `007`: no owner/group permissions, all permissions for others |
| [`9-John_Doe`](9-John_Doe) | Sets `hello` to mode `753`: owner `rwx`, group `r-x`, others `-wx` |
| [`10-mirror_permissions`](10-mirror_permissions) | Copies permission bits from `olleh` to `hello` using `chmod` reference mode |
| [`11-directories_permissions`](11-directories_permissions) | Recursively adds `a+X` below the current directory, including `.` |
| [`12-directory_permissions`](12-directory_permissions) | Creates `my_dir` with requested mode `751`: owner `rwx`, group `r-x`, others `--x` |
| [`13-change_group`](13-change_group) | Changes the group of `hello` to `school` |
| [`14-change_owner_and_group`](14-change_owner_and_group) | Changes ownership to `vincent:staff` for entries matched by `*` |
| [`15-symbolic_link_permissions`](15-symbolic_link_permissions) | Changes the owner/group of symbolic link `_hello` itself to `vincent:staff` |
| [`16-if_only`](16-if_only) | Changes the owner of `hello` to `vincent` only if its current owner is `guillaume` |

## Requirements

- Bash and GNU/Linux utilities supporting reference-mode `chmod` and the
  ownership options used in the scripts.
- Task accounts and groups where required: `betty`, `vincent`, `guillaume`,
  `school`, and `staff`.
- Appropriate permissions for the operation. Ownership changes typically
  require elevated privileges; `su` may request authentication.
- Disposable task files such as `hello`, `olleh`, and the `_hello` symbolic link.

These names are exercise inputs. The scripts do not create the users or groups.

## Syntax checks

From the repository root:

```bash
cd permissions
for script in [0-9]*; do
    bash -n "$script"
done
```

All 17 scripts pass Bash syntax checks locally. This does not establish that
the named accounts exist or that an ownership change is permitted.

## Usage

From this directory, inspect your current identity:

```bash
bash 1-who_am_i
bash 2-groups
```

The output depends on the account running the scripts.

To try file creation and permission changes in a disposable directory:

```bash
project_dir="$PWD"
practice_dir=$(mktemp -d)
cd "$practice_dir"
bash "$project_dir/4-empty"
bash "$project_dir/5-execute"
ls -l hello
cd "$project_dir"
```

`hello` remains in the temporary directory for inspection. Remove that sample
when finished:

```bash
rm -f "$practice_dir/hello"
rmdir "$practice_dir"
```

## Understanding the permission changes

- Numeric modes replace the relevant permission bits. Each octal digit uses
  read `4`, write `2`, and execute `1` for owner, group, and others respectively.
- Symbolic additions such as `u+x` preserve other existing permissions.
- Uppercase `X` applies execute/search permission to directories and to regular
  files that already have at least one execute bit. Task `11` can therefore
  change executable files as well as directories.
- Execute permission on a directory means the ability to search/traverse it;
  read permission controls listing its names.
- `0-iam_betty` opens another shell. Use `exit` to return to the original one.
- Task `14` uses a non-recursive `*` glob and omits hidden entries. Task `15`
  changes the symbolic link's ownership, rather than its target's ownership.

## Scope and verification

Relative paths are resolved from the caller's working directory. Task `11`
changes permissions recursively; ownership tasks can affect multiple entries.
Use a disposable exercise location with the expected accounts and privileges.

Local verification covered syntax and temporary-file permission changes.
Account switching and ownership exercises were not executed against the host's
users or project files. These short scripts do not add custom error handling.
