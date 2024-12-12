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

