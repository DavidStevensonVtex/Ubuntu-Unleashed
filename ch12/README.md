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

### Using Common Text Editors

Popular console-based text editors:

* emacs
* nano
* vim

Note that not all text editors are *screen oriented*, meaning designed for use from a terminal.

* gedit
* kate
* kedit

A good reason to learn how to use a text-based editor, such as `vi` or `nano`, is that system maintenance and recovery operations almost never take place during GUI sessions, negating the use of GUI editor.

Another reason to learn how to use a text-based editor under the Linux console is so that you can edit text files through remote shell sessions because many servers do not host graphical desktops.

`nano` and `vi` are almost universtally installed.

#### Working with `nano`

`nano` has the easiest learning curve.

`$ nano file.txt`

* Cursor movement - Arrow keys (left, down, up and right), Page Up and Page Down keys, `Ctrl+y` and `Ctrl+v` page up and down
* Add characters - type at the cursor location
* Delete character - backspace or Delete
* Exit - `Ctrl+x`
* Get Help - Ctrl+g

#### Working with `vi`

Chances are nearly 100% that `vi` will be available

`$ vi file.txt`

The `vi` command works by using an insert (or editing) mode and a viewing (or command) mode.

* Cursor movement - h, j, k, l (left, down, up and right)
* Delete character - x
* Delete line - dd
* Mode toggle - Esc, Insert (or i)
* Quit - :q
* Quit without saving :q!
* Run a shell command - :sh (use 'exit' to return)
* Save file - :w
* Text search

Use the `vimtutor` command to quickly learn how to use `vi`'s keyboard commands.

#### Working with `emacs`

Richard M. Stallman's GNU `emacs` editor, like `vi` is available with Ubuntu and nearly every other Linux distribution.

It's an editing environment, and you can use it to compile and build programs and act as an electronic diary, appointment book, and calendar.

`$ emacs file.txt`

If you start `emacs` using X11, the editor launches in its own floating window. To force `emacs` to display inside a terminal window instead of its own window, use the `-nw` command line option like this:

`$ emacs -nw file.txt`

#### Working with `sed` and `awk`

`sed`, which is short for *stream editor*, is a command that is used to perform transformations on text.

It works from the command line and processes text via standard in and standard out. It does not modify the original input and does not save the output unles you redirect the output to a file. It is most useful this way or when piped between other commands.

`awk` is a small programming languages for processing strings. It takes in text, transforms it in whatever way you tell it to, and then outputs the transformed text.

`sed` and `awk` aren't used much anymore, at least not by people who have entered the profession in the twenty-first century, but they are beloved by those who take the time to learn them.

```
$ sed sedcommand inputfile
$ sed -e sedcommand inputfile
$ sed -e sedcommand -e anothersedcommand inputfile

$ sed -e 's/camel/dune buggy/g' transportation.txt

# you can use a regular expression in place of line numbers
$ sed -e '4,17d' longtext.txt
```

You can use `sed` in scripts and chain commands together.

The most common use of `awk` is to manipulate files that consist of fields separated by delimters, such as comma-separated values (CSV) file output from a spreadsheet program or a configuration file that assigns default values to program variables.

You define the delimiter that `awk` will look for.

`$awk -F',' '{ print $1, "was last picked up on ", $4 } deskstuff.txt`

You can define multiple delimiters by using \[ \], like this: `-F'[;,-]'`.

### Working with Compressed Files

* bunzip2 - Expands a compressed file
* bzip2 - Compresses or expands files and directories
* gunzip - Expands a compressed file
* gzip - Compresses or expands file and directories
* tar - Creates o, expands or lists the contents of compressed or uncompressed file or directory archives known as tape archives or tarballs

To create a compressed archive of a directory, use `tar`'s `czf` options, like this:

`$ tar czf compressedfilename.tgz directoryname`

To list the contents of the compressed archive, substitute the `c` option with the letter `t`, like this:

```
$ tar tzf archive
$ tar tzf archive | less
```

To exapand the contents of a compressed archive, use `tar`'s zxf options, as follows:

`$ tar zxf archive`

### Using Multiple Terminals with `byobu`

Many Linux veterans have enjoyed and use the GNU `screen` command, which was designed to enable you to use on terminal to control several terminal sessions easily.

[GNU Screen](https://www.gnu.org/software/screen/)

*Byobu* is a Japanese term for decorative, multipanel, vertically folding screens that are often used as room dividers.

Like screen, byobu is a terminal multiplexer, which is a fancy term for a program that enables you to run multiple terminals inside one terminal.

* F2 - Creates a new window
* F3 - Goes to the previous window
* F4 - Goes to the next window
* F9 - Opens `byobu` menu for help and configuration

To close a terminal within `byobu`, simply log out of it normally, using `exit` or `Ctrl+D`.
When you exit the last terminal session that is open in `byobu`, the program closes as well
and drops you to the regular terminal session you used to start `byobu`.

However, there are two alternatives to quitting a `byobu` seession: locking and disconnecting.
* locking - activated with F12
* disconnecting - F6 - you can exit it and do other things for a while and then reconnect later

To reconnect, run the command `screen -r` or `byobu -r`.

* [byobu documentation](https://www.byobu.org/documentation)
* [Ubuntu byobu community](https://help.ubuntu.com/community/Byobu)

### Doing a Polite System Reset Using REISUB

Before you can use the REISUB feature, it must be enabled. The feature is enable when the value of /proc/sys/kernal/sysrq is set to 1. You must have this enabled before you encounter a problem in order for REISUB to work.

`cat /prod/sys/kernal/sysrq`

to change the value, first edit the /etc/sysctl.conf file by uncommenting the line in the file by removing the # in front of it and saving to set kernel.sysrq=1. Then run the following:

`sudo sysctl -p /etc/sysctl.conf`

REISUB is an acronym used as a nmenonic device to help users to remember the Magic SysRq Key sequence that is best to use when trying to restart a frozen system without risking damage to the file system. The SysRq key is under the Print Screen key on my keyboard.

You hold down SysRq+Alt and press the R, E, I, S, U, B keys one at a time, in order. Actions:

1. unRaw - takes control of the keyboard back from the X server
1. tEminate - Sends aSIGTERM command to all processes, which allows time for the processes to terminate gracefully
1. kIll - Sends a SIGKILL to all processes, forcing any that are still running to terminate immediately.
1. Sync - Flushese data from memory to disk
1. Unmount - Unmounts and remounts all file systems as read-only
1. reBoot - turns off and back on again, restarting the computer

If you have to use REISUB, allow several seconds for each step. Be patient. Doing it this way can save you from the heartache of lost data.

### Fixing an Ubuntu System that Will Not Boot

#### Checking BIOS

It is possible that you accidentally reset the boot devices and/or order in your system BIOS. If making sure those settings are correct does not help, you may have a hardware problem.

#### Checking GRUB

If you are able to turn on the computer on and get past the initial BIOS startup, then you should consider whether you can access GRUB.

Hold down the Shift key after the BIOS part is done to bring up the GRUB menu. If GRUB does not appear, then perhaps it has been overwritten, in which case the next section will help.

If GRUB is workign fine, skip to the "Using Recovery Mode" section.

#### Reinstalling GRUB

To restore GRUB, follow these steps:

1. Boot Ubuntu from a live DVD or bootable USB drive that has the same Ubuntu release as your system.

1. Determine the boot drive on your system:

    a. open a terminal and use `sudo fdisk -l` to list the drives attached to your system.

    b. Look for an entry with an * in the Boot column. This is your boot device. It will look something like /dev/sda1.

1. Mount the Ubuntu partition at /mnt by using this command, replacing /dev/sda1 with the information you just found:

    `sudo mount /dev/sda /mnt`

1. Reinstall GRUB with this command, again replacing /dev/sda1 with what you found earlier.

    `sudo grub-install --boot-directory=/mnt/boo /dev/sda1`

1. Restart the computer, and Ubuntu should boot properly.

#### Using Recovery Mode

Press Shift after the BIOS is done to access the GRUB menu. Select Advanced Options for Ubuntu.
From the new menu, select an entry with the words *recovery mode*. This boots into a recovery menu with options to automatically fix several possible problems, or at least it lets you boot into a minimal recovery-mode version of Ubuntu with only the most necessary processes loaded.

From here, you may be able to fix disks, check file systems, drop to a root prompt to fix file permissions, and so on.

#### Reinstalling Ubuntu

If you are able to boot using a live DVD or bootable USB drive using the same Ubuntu release or one just newer than the one on the hard drive, and if there are no hardware problems with your system, you can usually recover all your files by reinstalling Ubuntu.

### Tips and Tricks

#### Running the Previous Command

You can rerun the previous command with the up arrow and Enter, You can also rerun it with !! (referred to as "bang bang").

```
apt-get update
sudo !!
```

#### Running Any Previous Command

You can search your command history.

Type `Ctrl+R` at the command line to start what is called a "reverse-i search" and begin typing.
Whatever you type will be matched to previously run commands, so if you know it was a cool combination of commands piped together that had sort in the middle, start typing "sort" and watch as the displayed commands from your history appear.

#### Running a Previous Command that Started with Specific Letters

`!ls`

