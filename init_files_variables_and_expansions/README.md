# Shell Variables and Expansions

Fifteen Bash scripts practise aliases, environment variables, shell variables,
arithmetic expansion, brace expansion, and formatted output. The input values
for the arithmetic tasks come from named variables rather than user prompts.

## Scripts

| Script | What it does |
| --- | --- |
| [`0-alias`](0-alias) | Defines `ls` as the alias `rm -f *` in the shell that reads it |
| [`1-hello_you`](1-hello_you) | Prints `hello` followed by `$USER` |
| [`2-path`](2-path) | Appends `/action` to `PATH` and exports it |
| [`3-paths`](3-paths) | Counts non-empty colon-separated entries in `PATH` |
| [`4-global_variables`](4-global_variables) | Lists exported environment variables using `env` |
| [`5-local_variables`](5-local_variables) | Uses `set` to list shell variables and function definitions |
| [`6-create_local_variable`](6-create_local_variable) | Assigns the shell variable `BEST` the value `School` |
| [`7-create_global_variable`](7-create_global_variable) | Assigns `BEST=School` and exports it to child processes |
| [`8-true_knowledge`](8-true_knowledge) | Prints `TRUEKNOWLEDGE + 128` |
| [`9-divide_and_rule`](9-divide_and_rule) | Prints the integer quotient `POWER / DIVIDE` |
| [`10-love_exponent_breath`](10-love_exponent_breath) | Prints `BREATH` raised to the power `LOVE` |
| [`11-binary_to_decimal`](11-binary_to_decimal) | Interprets `BINARY` as base 2 and prints its decimal value |
| [`12-combinations`](12-combinations) | Prints the 676 lowercase two-letter combinations except `oo`, giving 675 lines |
| [`13-print_float`](13-print_float) | Prints `NUM` to two decimal places |
| [`14-decimal_to_hexadecimal`](14-decimal_to_hexadecimal) | Prints `DECIMAL` in lowercase hexadecimal |

## Requirements

- Bash and the `#!/bin/bash` interpreter used by the scripts.
- Standard Linux tools, including `env`, `tr`, `grep`, and `wc`.
- Numeric variables set to appropriate values for arithmetic tasks.

Brace expansion and the arithmetic expressions here are Bash features. Run the
scripts with Bash rather than assuming another shell behaves identically.

## Syntax checks

From the repository root:

```bash
cd init_files_variables_and_expansions
for script in [0-9]*; do
    bash -n "$script"
done
```

All 15 scripts pass Bash syntax checks locally. This does not execute the
commands or check the supplied numeric values.

## Usage

From this directory, pass input values through the environment:

```console
$ USER=student bash 1-hello_you
hello student
$ TRUEKNOWLEDGE=1209 bash 8-true_knowledge
1337
$ POWER=42784 DIVIDE=32 bash 9-divide_and_rule
1337
$ BREATH=4 LOVE=3 bash 10-love_exponent_breath
64
$ BINARY=1010 bash 11-binary_to_decimal
10
$ NUM=3.14159 bash 13-print_float
3.14
$ DECIMAL=255 bash 14-decimal_to_hexadecimal
ff
```

Check the combination count with:

```bash
bash 12-combinations | wc -l
```

It prints a count of `675`; the exact padding around `wc` output can vary.

## Shell state and limits

- Running a script with `bash` creates a child shell. Its assignments and
  aliases do not change your current shell. To keep the `BEST` assignment in
  your session, use `source ./6-create_local_variable` or
  `source ./7-create_global_variable`.
- The first assignment is a regular shell variable, not a function-local
  variable declared with Bash's `local` keyword. The exported assignment is
  also available to child processes.
- `0-alias` is a deliberately destructive alias exercise: if used in a shell
  where the alias expands, `ls` runs `rm -f *` and removes matching files.
  Do not source it in your normal working session. Inspect its definition or
  use an isolated disposable shell to study it.
- Sourcing `2-path` changes the current shell's `PATH`. Repeating it appends
  `/action` repeatedly; it does not check whether that directory exists.
- `3-paths` counts entries, not distinct existing directories, and ignores
  empty entries even though those can represent the current directory in PATH.
- Arithmetic uses Bash integer rules. Use valid numbers, a nonzero `DIVIDE`,
  and values small enough to avoid overflow. Float formatting can depend on
  the numeric locale.
