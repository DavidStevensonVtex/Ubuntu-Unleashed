# Ubuntu Unleashed, 2019 Edition

## Chapter 14: Automating Tasks and Shell Scripting

### Scheduling Tasks

Three ways to schedule commands:

1. `at` command, which specifies a command run at a specific time and date relativet to today.
1. `batch` command, which is actually a script that redirects you to the at command with some extra options set so your command runs when the system is quiet.
1. `cron` daemon, which is the Linux way of executing tasks at a given time 

#### Using `at` and `batch` to Schedule Tasks for Later

If you want to run a time-intensive task, but you do not want to do it while you are logged in, you can 
tell Ubuntu to run it later with the `at` command, which you must install.

To use `at`, you need to tell itthe time at which you want the task to run and then press Enter.

Run at just after 8:00 pm

```
at now + 7 hours
wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.0.tar.bz2
tar xvfjp linux-3.0.tar.bz2
<EOT>
```

You can use the `-f` parameter to have `at` read its commands from a file, like this:

```
echo wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.0.tar.bz2 \;
tar xvfjp linux-3.0.tar.bz2> myjob.job
at -f myjob.job tomorrow
```

* You can specify the number of minutes, hours, days or weeks relative to the current time.
* You can also specify several special times, including *tomorrow*, *midnight*, *noon*, or *teatime* (4 pm).
* You can specify an exact date and time using *HH:MM MM/DD/YY* format.

When you schedule a job using `at`, it is placed into queue "a" by default, which means it runs at your specified time and takes up normal amount of resources.

`batch` is really just a shell script that calls `at` with a few extra options.

* -q b - run job on queue b
* -m - mail the user on completion
* run immediately (now)

Jobs on queue b will only be executed when system load falls below 0.8 - thatis, when the system is not running at full load.

Queue jobs normally have a niceness of 2, whereas b queue jobs have a niceness of 4.
Queue c runs at a niceness 6, queue d runs at niceness 8, and so on.

When you submit a job for execution, you are also returned a job number.

If you want to see a list of other jobs you have scheduled to run later, use the `atq` command with no parameters.

If you want to delete a job, use the `atrm` command followed by the ID number of the job you want to delete.

The default configuration for `at` and `batch` is to allow everyone to use it, which is not always the desired behavior. Access is controlled through two files: `/etc/at.allow` and `/etc/at.deny`.

The `at.allow` file does not exist by default. If you have a blank `at.allow` file, no one except root is allowed to schedule jobs.

#### Using `cron` to Run Jobs Repeatedly

The `at` and `batch` commands work well if you just want to execute a single task at a later date, but thye are less useful if you want to run a task frequently.

Users listed in the cron.deny file are not allowed to use `cron`, and users listed in the `cron.allow` file are.

An empty `cron.deny` file -- the default -- means everyone can set jobs.
An empty `cron.allow` file means that no one (except root) can set jobs.

Two types of jobs:
* system jobs
* user jobs

Only root can edit *system* jobs, whereas any user whose name appears in a `cron.allow` or does not appear in `cron.deny` can run *user* jobs.

System jobs are controlled through the `/etc/crontab` file.

The `cron` daemon reads all the system crontab files and all the user crontab files once a minute to check for changes. However, any new jobs it finds will not be executed until at least 1 minute has passed.

You can also specify day and month names rather than numbers, using three-character abbreviations: Sun, Mon, Tue, Fri, Sat for days, Jan, Feb, Mar, Oct, Nov, Dec for months.

User jobs are stored in the /var/spool/cron diretory, which each user having his own file named after his username.

To edit your own `crontab` file, type `crontab -e`. This brings up a text editor, where you can enter your entries. By default the editor is vim, also known as vi.

When programming, we tend to use a `sandbox` subdiretory in our home diretory where we keep all sorts of temporary files that we were just playing around with.

If you are not allowed to schedule jobs, you will be stopped from editing your crontab file.

You can use the command `crontab -l` to list your jobs.

Use `crontab -e` to edit your crontab file. Ifyou want to delete all your jobs, you can use `crontab -r` to delete your `crontab` file.

#### Using `rtcwake` to Wake Your Computuer from Sleep Automatically

Wake your computer every hour.

`sudo rtcwake -m mem -s -3600`

`sudo rtcwake -m [type of suspend] -s [number of seconds]`

Five types of suspend:

* disk - (hibernate) The current state of the computer is written to disk, and the computer is powered off.
* mem - (sleep) The current state of the computer is written to RAME and the computer is put into a low-power state.
* no - The computer is not suspended immediately. Only wakeu time is set. This allows yo to continue working; you have to remember to put the computer to sleep manually.
* off - The computer is turned off completely. Wake will not work with this setting.
* standby - The computer is put into standby mode, which saves some power over running normally but not nearly as much as the other options.

### Basic Shell Control

* bash - Bourne Again Shell, /bin/bash
* ksh - Korn Shell, /bin/ksh, /usr/bin/ksh
* pdksh - A symbolic link to ksh, /usr/bin/pdksh
* rsh - restricted shell (for network operation), /usr/bin/rsh
* sh - A symbolic link to bash, /bin/sh
* tcsh - A csh-compatible shell, /bin/tcsh
* zsh - A shell compatible with csh, ksh, and sh, /bin/zsh

#### The Shell Command Line

* Searching files or directories
* Gettign data from and sending data to a file or command, input and output redirection.
* Feeding or filtering a program's output to another command (called using *pipes*)
* job control commands

`w; free; df`

Using the backslash as a line continuation
```
echo "this is a long \
command line and" ; echo "shows that multiple commands \
may be strung out."
```

*Mastering Regular Expressions* by Jeffrey E. F. Friedl

#### Shell Pattern-Matching Support

* \* - matches any character.

    `ls *.txt`

* \? - matches a single character.

    `ls *.d?c`

* \[xxx\] - Matches a range of characters

    `ls *[0-9]*`

*   \\x - matches or escapes a character such as ? or a tab character

    `touch foo\?`

#### Redirecting Input and Output

Special characters: \>, \<, or \>\>

`ls *.txt > textfiles.listing`

Use output rediretion with care because it is possible to overwrite existing files.

The shell can warn when attempting to redirect to a directory.

```
mkdir foo
ls > foo
```

Appending:

`ls *.text >> textfiles.listing`

Reading from standard input:

`cat < textfiles.listing`

You can use the shell *here* operator, \<\<, to specify the end of input on the shell command line:

cat \> simple_script  \<\< DONE
echo ""This is a simple script""
DONE

#### Piping Data

```
find /d2 -name '*.txt' -print | xargs cat | \
tr ' ' '\n' | sort | uniq > output.txt
```

#### Background Procesing

the shell alows you to start a command and then launch it into the background as a process by using an ampersand (\&) at the end of a command line.

`xterm &`

The numbers echoed back show a number, which is a job number or a reference number for a shell process, and a process ID number or PID.

Kill a job:

`kill %3`

Kill a process

`kill 1437`

`tar -czf /backup/home.tgz /home &`

### Writing and Executing a Shell Script

#### Running the New Shell Program

`./myenv.sh`

`ksh myenv.sh`

```
mkdir bin
mv myenv.sh bin
myenv.sh
```

`env | fgrep PATH`

`echo $PATH | tr ':' '\n'`

#### Storing Shell Scripts for System-wide Access

You can put new commands in `/etc/bashrc`. 

#### Interpreting Shell Scripts Through Specific Shells

The majority of shell scripts use a *shebang line* (#!) at the beginning to control the type of 
shell used to run the script; this bang line calls for an sh-incantation of `bash`:

`#!/bin/sh`
A shebang lin (it is short for "sharp" and "bang", two names for # and !) tells the Linux kernel 
that a specific command (a shell, or in the case of other scripts, perhaps *awk* or Perl) is to 
be used to interpret the contents of the file.

/bin/sh is a link to the Dash shell.

```
$ ll /bin/sh
lrwxrwxrwx 1 root root 4 Jul 18  2019 /bin/sh -> dash*
```

/bin/bash is a link to the Bash shell

The Shebang Line

The Shebang line is a magic number.

Avoiding the use of specific pathnames to programs increases shell script portability because 
not every UNIX or Linux system has programs in the same location.

Using Variables in Shell Scripts
* Environment Variables
* Built-in variables - unlike environment variables, you cannot modify built-in variables.
* User variables - Thse variables are defined with a script when you write a shell script.

#### Assigning a Value to a Variable

* bash: lcount=0 (no spaces!)
* tcsh: set lcount=0

* bash: myname=Sedona
* tcsh: set myname=Sedona

* bash: lcount=$var
* tcsh: set lcount=$var

#### Positional Parameters

The first parameter is stored in a variable called 1 (number 1) can be accessed by using `$1` within the program.

The second parameter is stored in a variable called `2` and can be accessed by using `$2` within the program, and so on.

#### A Simple Example of a Positional Parameter

```
#!/bin/sh
# Name display program
if [ $# -eq 0 ]
then
    echo "Name not provided"
else
    echo "Your name is "$1
fi

# Output

# bash mypgml
# Name not provided

# bash mypgml Sandra
# Your name is Sandra
```

#### Using Positional Parameters to Access and Retrieve Variables from the Command Line

Shell scripts that contain positional parameters are often used for automating routing and mundane jobs.

#### Using a Simple Script to Automate Tasks

#### Built-in Variables

* `$*` - The number of positional parameters passed to the shell program
* `$?` - The completion code of the last command or shell program executed within the shell program (returned value)
* `$0` - The name of the shell program
* `$*` - A single string of all arguments passed at the time of invocation of the shell program

#### Special Characters

* `$` - Indicates the beginning of a shell variable name
* `|` - Pipes standard output to the nextcommand
* `#` - Starts a comment
* `&` - Executes a process in the background
* `?` - Matches one character
* `*` - Matches one or more characters
* `>` - Redirects output
* `<` - Redirects input
* \` - Indicates command substitution
* `>>` - Redirects output (to append to a file)
* `<<` - Waits until the following end-of-input string (HERE operator)
* `[ ]` - Specifies a range of characters
* `[a-z]` - Specifies characters a through z
* `[a,z] or [az]` - Specifies characters a or z
* `Space` - Acts as a delimiter between two words

A few special characters deserve special note: double quotes ("), single quoets ('), backslash (\), and backtick (`).

##### Using Double Quoes to resolve Variables in Strings with Embedded Spaces

If a string contains embedded spaces, you can enclose the string in double quotes (") so that the shell interprets the whole string as one entity instead of as more than one.

Errors

```
$ x=abc def

Command 'def' not found, did you mean:
```

No error:

`x="abc def"`

```
var="test string"
newvar="Value of var is $var"
echo $newvar
# Output: Value of var is test string
```

##### Using Single Quotes to Maintain Unexpanded Variables

You can surround a string with single quotes (') to stop the shell from expanding variables and interpreting special characters.

When used for the latter purpose, the single quote is an *escape character*, similar to the backslash.

```
var='test string'
newvar='Value of var is $var'
echo $newvar
# Output: Value of var is $var
```

##### Using the Backslash as an Escape Character

```
test="abc def"
var=\$test
echo $var
# Output: $test
```

##### Using the Backtick to Replace a String with Output

You can use the backtick (`) character to signal the shell to replace a strign with its output when executed. This is called *command substitution*.

```
echo "abc def ghi jkl mno" > test.txt
var=`wc -w test.txt`
echo "$var words"
# Output: 5 test.txt words
```

#### Comparison of Expressions in `pdksh` and `bash`

`test expression` 
or
`[ expression ]`

##### String Comparison

* = - Compares whether two strings are equal
* != - compares whether two strings are not equal
* -n - Evaluates whether the string length is greater than zero
* -z - Evaluates whether the string length is equal to zero

##### Numeric Comparison

* `-eq` - Compares whether two numbers are equal
* `-ge` - Compares whether one number is greater than or equal to the other number
* `-le` - Compares whether one number is less than or equal to the other number
* `-ne` - Compares whether two numbers are not equal
* `-gt` - Compares whether one number is greater than the other number
* `-lt` - Compares whether one number is less than the other number

##### File Operators

* `-d` - Determines whether a file is a directory
* `-f` - Determines whether a file is a regular file
* `-r` - Determines whether read permission is set for a file
* `-s` - Determines whether a file exists and has a length greater than zero
* `-w` - Determines whether write permission is set for a file
* `-x` - Determines whether execute permission is set for a file

#### The `for` Statement

```
for curvar in list
do
    statements
done

# statements are executed once for each of the positional parameters passed to the shell program.
for curvar
do
    statements
done

# You can also write this format as follows:
for curvar in $
do
    statements
done
```

#### The `while` statement

You can use the `while` statement to execute a series of commands while a specified condition is `true`.
The loop terminates as soon as the specified condition evalutes to `false`.

You should be careful with the `while` command because the loop never terminates if the specified condition never evaluates to `false`.

```
while expression
do
    statements
done
```

#### The `repeat` Statement

`repeat 80 echo -n '-'`

#### The `shift` statement

You use the `shift` statement to process the positional parameters, one at a time, from left to right.
Recall that the positional parameters are identified as $1, $2, $3 and so on.
The effect of the shift command is that each positional parameter is moved one position to the left, and the current $1 parameter is lost.

The `shift` statement is useful when you are writing shell programs in which a user can pass various options.

The format of the shift command is as follows:

`shift number`

If the number is not specifed, the default is 1.

