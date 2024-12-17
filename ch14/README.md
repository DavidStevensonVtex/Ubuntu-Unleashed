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