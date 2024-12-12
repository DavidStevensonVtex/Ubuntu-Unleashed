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

