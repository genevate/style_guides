# Bash Shell Script Styles

## General

- Use environment variables instead of process output:
    - Yes: $PWD
    - No: $(pwd)
- Use `$((...))` instead of `expr` when executing arithmetic expressions.
- Use 1/0 instead of true/false for boolean variables.
- Use quotes around every `"$variable"` and `"$(...)"` expression unless word-spliting and/or glob interpretation is
  required.

## Settings

- The first line of every Bash script should be: `#!/bin/bash`.
- Avoid using `#!/bin/sh` unless the script is runnable and testable on the following systems:
    - Sh.
    - Dash in POSIX-compatible mode (Debian).
    - Bash in POSIX-compatible mode (OSX).
- Use the following at the top of every script:

        set -o nounset # Exit (non-zero) when referencing undefined variables (Shortcut: -u, Default: '').
        set -o errexit # Exit (non-zero) when any command fails (Shortcut: -e, Default: false).
        set -o pipefail # Exit (non-zero) when rightmost piped command fails (otherwise zero if all pipes pass).

## Variables

- The following global variables are available:
    - $0 = The script name.
    - $n = The positional parameters.
    - $$ = The script PID.
    - $! = The PID of the last command executed (and run in the background).
    - $? = The exit status of the last command (Use ${PIPESTATUS} for pipelined commands).
    - $# = The number of parameters.
    - $@ = All parameters (interprets each argument as a separate word). NOTE: Handles empty arguments and whitespace
      within arguments. Should be quoted: "$@".
    - $- = All parameters (interprets all arguments as single word). WARNING: This is rarely the right choice, use $@
      instead.
- When declaring variables, use the following annotations:

        local <variable> # For local variables inside a function.
        readonly <variable> # For variables that are readonly (can also be applied after a variable is defined).

## Strings

- Use `${<variable>,,}` to convert a string to lowercase. Example:

        example="TEST"
        printf "${example,,}\n" # "test"
- Use `${<variable>^^}` to convert a string to uppercase. Example:

        example="test"
        printf "${example^^}\n" # "TEST"
- Use `${#<variable>}` to get string length:

        example="some/path/to/file.txt"
        printf "${#example}\n" # 21

- Use `${<variable>:<start>}` to slice a string from a starting position:

        example="This is a test."
        printf "${example:10}\n" # "test."
        printf "${example: -5}\n" # "a test."

- Use `${<variable>:<start>:<length>}` to slice a string from a starting position to a given length:

        example="This is a test."
        printf "${example:5:4}\n" # "is a"

        start=2
        length=5
        printf "${example:${start}:${length}}\n" # "is is"

- Use `/` to substitute a single string:

        example="This is a test."
        printf "${example/This/Here}\n" # "Here is a test."

- Use `//` to substitute global strings:

        example="This is a test."
        printf "${example//is/IS}\n" # "ThIS IS a test."

- Use `//` and a variable to split a string into an array:

        example="some/path/to/file.txt"
        readonly SEPARATOR='/'
        array=(${example//${SEPARATOR}/ })
        printf "${array[3]}\n" # "file.txt"

- Use `${<variable>#*<match>}` to substring after match of string:

        example="some/path/to/file.txt"
        printf "${example#*.}\n" # "txt"

- Use `${<variable>##*<match>}` to substring (greedy) after match of string:

        example="some/path/to/file.txt"
        printf "${example##*/}\n" # "file.txt"

- Use `${<variable>%<match>*}` to substring from beginning to match of string:

        example="some/path/to/file.txt"
        printf "${example%/*}\n" # "some/path/to"

- Use `${<variable>%%<match>*}` to substring (greedy) from beginning to match of string:

        example="some/path/to/file.txt"
        printf "${example%%/*}\n" # "some"

## Here Documents

- Use a marker for multi-line strings (with variable substituion):

        command << EOS
        "Line 1"
        ${variable}
        EOS

- Use a "marker" for multi-line strings (without variable substituion):

        command << "EOS"
        "Line 1"
        "Line ${variable}. This entire line will not be substituted."
        EOS

## Conditionals

- Use `[[  ]]` instead of `[ ]`. The former avoids issues with unexpected pathname expansion and adds
  syntactical/readable functionality.
      - Syntax:

            ||  # Logical OR.
            &&  # Logical AND.
            <   # String comparison without escaping.
            -eq # Numerical equality.
            -ne # Numerical inequality.
            -lt # Numerical less than comparison.
            -le # Numerical less than or equal to comparison.
            -gt # Numerical greater than comparison.
            -ge # Numerical greateer than or equal to comparison.
            ==  # String matching with globbing.
            =~  # String matching with regular expressions.
            -n  # Non-empty string.
            -z  # Empty string.
      - Examples:

            example="abc123"
            [[ "$example" == abc- ]]         # true (globbing)
            [[ "$example" == "abc*" ]]       # false (literal matching)
            [[ "$example" =~ [abc]+[123]+ ]] # true (regular expression)
            [[ "$example" =~ "abc*" ]]       # false (literal matching)
      - Notes:
          - With Bash 3.2+, regular/glob expressions must be quoted.
          - Use variables if the expression contains whitespace. Example:

                    examle="a b+"
                    [[ "a bbb" =~ $example ]] # true
- Check for exit statuses instead of output:
    - Yes: `if git status;`.
    - No: `if [ -n "$(git status)” ];`.

## Loops

- Use `for..done` loops instead of `while read..done` loops.

## Cases

- Globs can be used in case statements:

        case $example in
          abc*) <action>;;
          xyz*) <action>;;
          *) <action>;;
        esac

## Searches

- Use `grep -c` instead of `grep | wc -l`.

## Subshells

- Use `$()` instead of `` for capturing command output or command substitution. The former is easier to read and allows
  nesting of commands.

## Errors

- When dealing with failing commands, use the following to catch and log the error:

        if ! <flaky command> ; then
          printf "Failure Ignored.\n"
        fi

## Debugging

- Use `bash -n <script>` to perform a check/dry run of the script:
- Use `bash -v <script>` to yield a stack trace of the script. NOTE: The global setting is: `set -o verbose`
- Use `bash -x <script>` to yield a stack trace of the script including expanded commands. NOTE: The global setting is:
  `set -o xtrace`

## Output

- Use `printf` instead of `echo`.

## Files

- Avoiding parsing `ls` output as UNIX systems allow any character in a file name which makes finding the delimiter
  extremely difficult and error prone. Details [here](http://mywiki.wooledge.org/ParsingLs). Use `for` loops instead:

        for file in *; do
            [[ -e $file ]] || continue
            ...
        done
- Avoid using `cat` to provide file contents to `stdin` to a command/process that accepts file arguments.
- Use `mktemp` instead of `$$` to create a temporary file.
- Use `<()` to avoid creating temporary files for commands that expect file arguments when piping:

        diff <(curl --location url_1) <(curl --location url_2)

## Resources

- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bashref.html).
- [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html).
- [Better Bash Scripting in 15 Minutes](http://robertmuth.blogspot.com/2012/08/better-bash-scripting-in-15-minutes.html).
- [Thoughtbot Guides](https://github.com/thoughtbot/guides).
