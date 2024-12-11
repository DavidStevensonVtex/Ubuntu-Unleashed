# Ubuntu Unleashed, 2019 Edition

## Chapter 11: Command-Line Master Class, Part 1

### Why Use the Command Line?

* You want to chain together two or more commands.
* You want to use a command or parameter available only on the shell.
* You are working on a text-only system.
* You have used it for along time and feel comfortable there.
* You want to automate a task.

### Using Basic commands

* cat - Prints the contents of a file
* cd - changes directories
* chmod - Changes file access permissions
* cp - Copies files
* du - Prints disk usage
* emacs - Edits text files
* find - Finds files by searching
* grep - Searches for a string in input
* less - Filters for paging through output
* ln - Creates links between files
* locate - Finds files from an index
* ls - Lists files iin the current diretory
* make - compiles and installs programs
* man - Displays manual pages for reading
* mkdir - Makes directories
* mv - Moves files
* nano - Edits text files
* rm - Deletes files and directories
* sort - Takes a text file as input and outputs the contents of the file in the order you specify
* ssh - Connects to other machines using a secure shell connnection
* tail - Prints the last lines of a file
* vim - Edits text files
* which - Prints the location of a command

Other commands:
* cut
* diff
* gzip
* history
* ping 
* su
* tar
* uptime
* who

`emacs`, `nano` and `vim` are text editors that have text-based interfaces all their own
and are covered later in this chapter.

`ssh` is covered in detail in Chapter 19 "Remote Access with SSH, Telnet and VNC".

### Printing the Contents of a File with `cat`

```cat myfile.txt```

```$ cat -sn /proc/cpuinfo```

You can use cat to concatenate the output of more than one file.

```cat -s myfile.txt myotherfile.txt```

### Changing Directories with `cd`

The first part of cd's magin lies in the characters `-` and `~` (dash and tilde). 
The minus sign says switch to my previous directory.
The tilde means my home directory.

```
cd somedir
cd /home/matthew/stuff/somedir
cd /usr/local
cd bin
cd -
cd ~
```