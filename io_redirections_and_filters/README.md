# Shell I/O Redirections and Filters

Twenty-three Bash scripts practise standard input and output, pipes, quoting,
file redirection, and text filters. Some read system files; others transform
text supplied through a pipe or change files in the current directory.

## Scripts

| Script | What it does |
| --- | --- |
| [`0-hello_world`](0-hello_world) | Prints `Hello, World` and a newline |
| [`1-confused_smiley`](1-confused_smiley) | Prints a smiley containing quotes, a backslash, and a non-ASCII character |
| [`2-hellofile`](2-hellofile) | Displays `/etc/passwd` |
| [`3-twofiles`](3-twofiles) | Displays `/etc/passwd` followed by `/etc/hosts` |
| [`4-lastlines`](4-lastlines) | Prints the last ten lines of `/etc/passwd` |
| [`5-firstlines`](5-firstlines) | Prints the first ten lines of `/etc/passwd` |
| [`6-third_line`](6-third_line) | Prints the third line of a file named `iacta`, when present |
| [`7-file`](7-file) | Creates or overwrites a specially quoted filename containing punctuation, with the text `Best School` |
| [`8-cwd_state`](8-cwd_state) | Writes `ls -la` output to `ls_cwd_content`, replacing previous contents |
| [`9-duplicate_last_line`](9-duplicate_last_line) | Appends the last line of `iacta` to that same file |
| [`10-no_more_js`](10-no_more_js) | Recursively deletes regular files whose names end in `.js` below the current directory |
| [`11-directories`](11-directories) | Counts descendant directories, including hidden ones, without counting `.` itself |
| [`12-newest_files`](12-newest_files) | Prints up to ten visible entries in modification-time order, newest first |
| [`13-unique`](13-unique) | Sorts standard input and prints only lines that occur exactly once |
| [`14-findthatword`](14-findthatword) | Prints lines containing `root` from `/etc/passwd` |
| [`15-countthatword`](15-countthatword) | Counts lines containing `bin` in `/etc/passwd` |
| [`16-whatsnext`](16-whatsnext) | Prints matching `root` lines and up to three following lines from `/etc/passwd` |
| [`17-hidethisword`](17-hidethisword) | Prints lines from `/etc/passwd` that do not contain `bin` |
| [`18-letteronly`](18-letteronly) | Prints lines beginning with an alphabetic character from `/etc/ssh/sshd_config` |
| [`19-AZ`](19-AZ) | Translates `A` to `Z` and `c` to `e` on standard input |
| [`20-hiago`](20-hiago) | Removes lowercase and uppercase `c` from standard input |
| [`21-reverse`](21-reverse) | Reverses the characters on each input line |
| [`22-users_and_homes`](22-users_and_homes) | Extracts usernames and home directories from `/etc/passwd`, separated by a colon, then sorts the lines |

## Requirements

- Bash and standard Linux tools such as `find`, `grep`, `sort`, `uniq`, `tr`,
  `cut`, `head`, `tail`, and `rev`.
- Read access to the system files used by the selected task. SSH server
  configuration is not installed on every machine.
- Disposable task files for exercises that create, overwrite, append, or delete.

The scripts use the caller's working directory for relative paths.

## Syntax checks

From the repository root:

```bash
cd io_redirections_and_filters
for script in [0-9]*; do
    bash -n "$script"
done
```

All 23 scripts pass Bash syntax checks locally. Parsing does not run their
commands or verify the existence of input files.

## Usage

From this directory:

```console
$ bash 0-hello_world
Hello, World
$ printf 'banana\napple\nbanana\npear\n' | bash 13-unique
apple
pear
$ printf 'Ac\n' | bash 19-AZ
Ze
$ printf 'Chocolate\n' | bash 20-hiago
hoolate
$ printf 'hello\n' | bash 21-reverse
olleh
```

Scripts that read standard input can also take redirected input:

```bash
bash 21-reverse < input.txt
```

Create `input.txt` with your own sample text before running that example.
For `6-third_line` and `9-duplicate_last_line`, provide a disposable file named
`iacta` in the working directory.

## Behavior and limits

- `13-unique` uses `uniq -u`, so repeated lines disappear entirely. It does
  not print one copy of every distinct line.
- `12-newest_files` uses `ls`, so its output can include directories and is
  not a robust machine-readable filename listing.
- `15-countthatword` counts matching lines, not every occurrence of `bin`.
  The grep searches match substrings, not specifically account names.
- `18-letteronly` reads the fixed SSH configuration path, not standard input.
- Scripts `7` and `8` can overwrite files, `9` changes its input file, and
  `10` deletes matching files recursively. Run them only in disposable task
  locations after checking their commands.
- System-file output and sorting/character classes can vary with the machine
  and locale. The scripts do not provide custom error handling.
