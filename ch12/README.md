# Ubuntu Unleashed, 2019 Edition

## Chapter 12: Command-Line Master Class, Part 2

* How to link commands together
* Three Most Popular Text Editors
    1. vim
    1. emacs
    1. nano
* Unix Tools
    1. sed
    1. awk

### Redirecting Output and Input

* standard input
* standard output

`cat /proc/cpuinfo > file.txt`

Be aware that you can overwrite the contents of a file by using a redirect in this manner.

`cat < file.txt`

Ubuntu uses a software packaging system called apt.

`sudo dpkg --get-selections > pkg.list`

`sudo dpkg --set-selections < pkg.list`

`sudo apt-get -u deselect-upgrade`

`cat myfile.txt myotherfile.txt > combinedfile.txt`

If you want to append information to the end of a text file, use the > redirect operator.

`echo "This is a new line being added." >> file.txt`

If you want to suppress the output from a process, redirect to /dev/null.

`verboseprocess > /dev/null`

### `stdin`, `stdout`, `stderr` and Redirection

```
Standard input, 0
Standard output, 1
Standard error, 2
```

Redirecting to Standard Error

`program 2> error.log`

Redirect both stderr and stdout to a file:

`program &> filename`

Append both stderr and stdout to a file:

`program >> filename 2>&1`

to redirect standard error to standard out:

`program 2>&1`

### Comparing Files

* what in the files are the same
* what in the files are different

#### Finding Differences in Files with `diff`

`diff file1 file2`

Command line options for diff:

* -i or -ignore-case
* -b or -ignore-space-change - Ignores changes in the amount of white space
* -w or -ignore-all-space - Ignore all white space
* -q or -brief - Outputs only whether the files differ
* -l or --paginate - Passes the output through pr to paginate it

#### Finding Similarities in Files with `comm`

The comm command compares files line by line and outputs any lines that are identical.

`comm file1 file2`

This is a much more detailed comparison than with `diff``, and the output can be overwhelming.

Some options when running `comm`:

* -1 - supresses the output of column 1
* -2 - supresses the output of column 2
* -3 - supresses the output of column 3

### Limiting Resource Use and Job Control

#### Listing Processes with `ps`

Parameter styles:
* UNIX style
* GNU style
* X style
* BSD style uses single letters without dashes

`ps` parameters
* a - life the only yourself restriction
* f
* x
* u
* +sort or -sort - options: command, cpu, pid, user, etc.

ps aux -sort=%cpu

#### Listing Jobs with `jobs`

If you are running an interactive program you can press `Ctrl-Z` to suspend it.
Then you can start it back in the foreground using `fg`, or in the background using `bg`.

You can also start a program running in the background by appending an & like this:

`programname &`

To list all the jobs you are running, you can use `jobs`:

```jobs```

Parameters for `jobs`:

* -1 - Lists the process IDs along with the normal output
* -n - Displays information only about jobs that have changed status since the user was last notified of the status
* -r - Restricts output to running jobs
* -s - Restricts output to stopped jobs

#### Running One or More Tasks in the Background

`command &`

A background process runs without any user input.

You can input a list of serveral commands to run in the background.

`a & b & c &`

You can even use pipes within background processes, and you can combine multiples of each.

`d & | e & f & g & | h &`

Commands that are piped together are treated as one process.

#### Moving Jobs to the Background or Foreground with `bg` and `fg`

*Foreground jobs* are process groups with control of the terminal.

*Background jobs* are process groups without control of the terminal.

`find ~ -type f -printf "%s\t%p\n" | sort -n`

You can press `Ctrl+Z` to suspend the job and then you type tyis:

`bg`

That causes the process to resume but this time running in the background.

Both `bg` and `fg`, if entered with no further arguments, operate on the job you have most recently connected with.

Remember that the `jobs` command lists all current jobs and their status (running, stopped, and so on).

Each job has a number. Use the job number to move a job to the foreground.

`fg %2`

If you want to move a specific job to the background, just add the job number the same way:

`bg %2`

If you want a job to continue after you exit, you should consider using a tool such as `byobu`, 
or learn to run the process as a daemon.

### Printing Resource Usage with `top`

The default sort order in top shows the most CPU-intensive tasks first.

Enter k to kill a process.

Enter f to choose the fields to display.

Fields Management for window 1:Def, whose current sort field is %CPU
   Navigate with Up/Dn, Right selects for move then `<Enter>` or Left commits,
   'd' or `<Space>` toggles display, 's' sets sort.  Use 'q' or `<Esc>` to end!

If you press B, text bolding is enabled.

`r` enables you to renice - or adjust the niceness value.
19 is the lowest and -19 is the highest. Anything less than 0 is 
considered "high" and should be used sparingly.

#### Setting Process Priority with `nice`

You can set the priority for individual processes to tell the kernel to either limit or give extra priority to a specific process.

 You can set the process priority when you first run a program by putting the command before whatevery you are going to run and assigning the process a value that designates its priority.

 By default, all processes start with a priority of 0 (zero). Nice can be set for a maximum of -20, which is the highest priority, to a minimum of 19, the lowest priority.

 `sudo nice -n 19 tar czf compressedfilename.tgz directoryname`

 If a process is already running, you can reset the priority (some say "renice it") by using `renice`.
 To adjust a specific process, first use `top` to learn the PID for the process and then use `-p PID`:

 `sudo renice 19 -p 20136`

 The renice command allows priority adjustments to be made on all processes owned by a specific user or group in the system.

```
sudo renice -20 -u mysql
sudo renice -20 -g website
```

With the `ionice` command, you can adjust priority for disk access.
There are only three class settings for priority: Idle(3, lowest), Effort(2, default),
and Real Time (1, highest priority).

The -c flag designates class.

`sudo ionice -c3 -p24351`

### Combining Commands

#### Pipes

`ps aux | grep nethack`

`ps aux | grep nethack | wc -l`

`find / -name "*.txt" -size +10k -user dstevenson -not -perm +o=r -exec chmod o+r {} \;`

`find / -name "*.txt" -size +10k -user dstevenson -not -perm +o=r | xargs chmod o+r`

The xargs -i parameter allows you to specify exactly where the matching lines should be placed in your command.

`find /home/dstevenson -size +10000k | xargs -i cp {} /home/dstevenson/archive`

`dpkg --get-selections | grep gnome | sort`

#### Combining Commands with Boolean Operators

If you want to run a second command only if the first command is successfully completed, you can.

Every command you issue to the system outputs an exit status: 0 for true (successfull) and 1 for false (failed).

`$ i && k`

You can do exactly the opposite with ||, which runs the following command only if the first one returns an exit status of 1 for false:

`$ m || n`

#### Running Separate Commands in Sequence

If you want to have a set of commands run in order but not use the output from one as the input to the next one, you can. Separating commands with a ; (semicolon)...

`$ doctor ; rose ; tardis`

#### Process Substitution

Sometimes the output of one or more commands is precisely what you want to use as the input to another command. You can use output redirection for this purpose, using what we call *process substitution*.
In process substitution, you surround one or more commands with \( \) and precede each list with a \<.

`$ cat < (ls -al)`

Same as:

`$ ls -al | cat`

In the following example, you take the output of two `ls` commands as input to a `diff` command to compare the contents of the two directories:

`$ diff < (ls firstdirectory) < (ls seconddirectory)`

Faster than doing  the following and also no need to clean up temporary files:

```
$ ls firstdirectory > file1.txt
$ ls secondirectory > file2.txt
$ diff file1.txt file2.txt
```

### Executing Jobs in Parallel

GNU parallel is a shell tool for executing jobs in parallel across multiple processors, cores, or even multiple connected computers.

[GNU parallel](https://www.gnu.org/software/parallel/)

### Using Environment Variables

*Environment variables* are in-memory variables that are assigned and loaded by default when you login, or can be assigned by terminal commands.

* `PWD`
* `USER`
* `LANG`
* `SHELL` - name and location of the current shell, such as /bin/bash
* `PATH`
* `TERM`

`echo $USER`

You can use `env` to display all environment variables defined.

```
$ env | grep USER
USERNAME=dstevenson
USER=dstevenson
```

Default settings for bash are stored in /etc/profile and /etc/bashrc as well as .bashrc or .bash_profile in your /home directory.

Commands are located by using the PATH environment variable, which is a colon separated list of directories to search for commands.

`echo $PATH | tr ":" "\n"`

```
$ whereis ls
ls: /bin/ls /usr/share/man/man1/ls.1.gz
/bin/ls
```
Adding /sbin to your search path in ~/.bashrc:

`PATH=/sbin:$PATH`

`source .bashrc # alternatively .bash_profile`

You can change to appearanche of you terminal prompt using the PS1 environment variable:

`export PS1='$OSTYPE r001z -> '`