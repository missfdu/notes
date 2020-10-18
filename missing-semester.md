## Missing Semester

### Course overview + the shell

`echo $PATH`

`which <program>` shows the path to the program file we want to execute

redirection: `< file` for input stream, `> file` for output stream, `>>` to append to a file

pipes: `|` operator lets you “**chain**” programs such that the output of one is the input of another

```
missing:~$ ls -l / | tail -n1
drwxr-xr-x 1 root  root  4096 Jun 20  2019 var
```

Operations like `|`, `>`, and `<` are done *by the shell*, not by the individual program. `echo` and friends do not “know” about `|`.This may lead to errors when root privilege is required.

`tee` : read from standard input and write to standard output and files  

Example: change the brightness of screen through a file called `brightness` under `/sys/class/backlight`

```bash
$ sudo echo 3 > brightness
An error occurred while redirecting file 'brightness'
open: Permission denied
$ echo 3 | sudo tee brightness
# to turn on the led of scrolllock key, use the command below
$ echo 1 | sudo tee /sys/class/leds/input23::scrolllock/brightness
```

### Shell Tools and Scriping

#### Assign variables in bash

eg. `foo=bar` (**no spaces!**,or it will be interpreted as calling `foo` program with two arguments.)

In shell scripts the space character will perform argument splitting.

#### Strings: two ways to define

Strings delimited with `'` are literal strings and will not substitute variable values whereas `"` delimited strings will.

```bash
foo=bar
echo "$foo"
# prints bar
echo '$foo'
# prints $foo
```

#### Functions

```bash
mcd () {
    mkdir -p "$1"
    # Here $1 is the first argument to the script/function
    cd "$1"
}
```

Unlike other scripting languages, bash uses a variety of special variables to refer to arguments, error codes, and other relevant variables. Below is a list of some of them. ([Comprehensive list here](https://www.tldp.org/LDP/abs/html/special-chars.html))

- `$0` - Name of the script
- `$1` to `$9` - Arguments to the script. `$1` is the first argument and so on.
- `$@` - All the arguments
- `$#` - Number of arguments
- `$?` - Return code of the previous command
- `$$` - Process identification number (PID) for the current script
- `!!` - **Entire last command**, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; you can quickly re-execute the command with sudo by doing `sudo !!`
- `$_` - **Last argument from the last command**. If you are in an interactive shell, you can also quickly get this value by typing `Esc` followed by `.`

#### Command substitution

You can **get the output of a command as a variable** by placing commands in `$( CMD )`

 A lesser known similar feature is ***process substitution***.`<( CMD )` will execute `CMD` and place the output in a temporary file and substitute the `<()` with that file’s name.This is useful when commands **expect values to be passed by file** instead of by STDIN.


Since that was a huge information dump, let’s see an example that showcases some of these features. It will iterate through the arguments we provide, `grep` for the string `foobar`, and append it to the file as a comment if it’s not found.

```bash
#!/bin/bash

echo "Starting program at $(date)" # Date will be substituted

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # When pattern is not found, grep has exit status 1
    # We redirect STDOUT and STDERR to a null register since we do not care about them
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

#### Shell *globbing*

- Wildcards: `?` and `*` to match one or any amount of characters respectively

- Curly braces`{}`: Whenever you have a common substring in a series of commands,use curly braces for bash to expand this automatically.

```bash
convert image.{png,jpg}
# 会展开为
convert image.png image.jpg
# 也可以结合通配使用
mv *{.py,.sh} folder
# 会移动所有 *.py 和 *.sh 文件
```

#### Finding files

`find`

```bash
# Find all directories named src
find . -name src -type d
# Find all python files that have a folder named test in their path
find . -path '*/test/*.py' -type f
# Find all files modified in the last day
find . -mtime -1
# Find all zip files with size in range 500k to 10M
find . -size +500k -size -10M -name '*.tar.gz'
# Delete all files with .tmp extension
find . -name '*.tmp' -exec rm {} \;
# Find all PNG files and convert them to JPG
find . -name '*.png' -exec convert {} {}.jpg \;
```

`fd PATTERN`:a simple, fast, and user-friendly alternative to `find`

`locate`

`locate` uses a database that is updated using [`updatedb`](https://www.man7.org/linux/man-pages/man1/updatedb.1.html).In most systems, `updatedb` is updated daily via [`cron`](https://www.man7.org/linux/man-pages/man8/cron.8.html).herefore one trade-off between the two is **speed vs freshness**.

Moreover `find` and similar tools can also find files using attributes such as file size, modification time, or file permissions, while`locate` just uses the file name.

#### Finding code

`grep`: generic tool for matching patterns from the input text

- `-C ` for getting **C**ontext around the matching line.  e.g. `grep -C 5` will print 5 lines before and after the match
- `-v` for in**v**erting the match,print all lines that do **not** match the pattern
- `-R` will **R**ecursively go into directories and look for files for the matching string

`grep` alternatives:[ack](https://beyondgrep.com/), [ag](https://github.com/ggreer/the_silver_searcher) and **[rg]**(https://github.com/BurntSushi/ripgrep)

```bash
# Find all python files where I used the requests library
rg -t py 'import requests'
# Find all files (including hidden files) without a shebang line
rg -u --files-without-match "^#!"
# Find all matches of foo and print the following 5 lines
rg foo -A 5
# Print statistics of matches (# of matched lines and files )
rg --stats PATTERN
```

#### Finding shell commands

`history` print your shell history to the standard output. We can pipe that output to `grep` and search for patterns like`history | grep find`

In most shells, you can make use of `Ctrl+R` to perform backwards search through your history.

If you start a command with a **leading space** it won’t be added to your shell history. This comes in handy when you are typing commands with **passwords** or other bits of **sensitive** information.

#### Directory Navigation



### Vim



### Data Wrangling