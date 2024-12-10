# Ubuntu Unleashed - 2019 Edition

My self-training in Ubuntu Unleashed - 2019 Edition

This covers versions 18.04, 18.10, 19.04 and 19.10

## Chapter 1: Installing Ubuntu and Post-Installation Configuration

[Unified Extensible Firmware Interface](https://help.ubuntu.com/community/UEFI)

### Partioning

The easiest and simplest method is to use GParted, which is a graphical partition manager.
GParted is not installed by default, but it is available in the Ubuntu software repositories;
see Chapter 9, "Managing Software," if you need help installing it.

In addition to being useful for adding drives, GParted can also assist you in recovering
from problems. You can run it after booting Ubuntu in a live session or running from a
live CD or a USB drive.

### Shutting down Using the Command Line

```
sudo shutdown -h now

or

sudo shutdown -r now
```

### Software Updater

Click Activities and search for software updater

```
sudo apt update

sudo apt-get update

```

For a full upgrade:

```
sudo apt full-upgrade
```

### What version of Ubuntu am I running?

I just upgraded to Ubuntu 20.04

```
lsb_release -a
dstevenson@dstevensonlinux1:~/Ubuntu$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 20.04.6 LTS
Release:	20.04
Codename:	focal
```

```
cat /etc/os-release
dstevenson@dstevensonlinux1:~/Ubuntu$ cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.6 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.6 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

### Configuring User Name and Email in Git

```
git config --global user.name "David Stevenson"
git config --global user.email "drstevenson1958@yahoo.com"
git config --list
```

### The sudo Command

```sudo command commandoptions```

Login as root
```sudo -i```

### Using the hwclock command to set system time

```
sudo hwclock --show
sudo hwclock --set --date "09/28/18 10:33:00"
```

### Troubleshooting Post-Installation Configuration Problems

```
dmesg > dmesg.txt
less dmesg.txt
```

## Chapter 2: Background Information and Resources

```
uname -v -r
5.4.0-200-generic #220-Ubuntu SMP Fri Sep 27 13:19:16 UTC 2024
```

### Linux Guides and Books

[Advanced Bash-Scripting Guide, by Mendel Cooper](https://tldp.org/LDP/abs/html/)

[LDP Author Guide, by Mark F. Komarinksi and others](http:www.tldp.org/LDP/LDP-Author-Guide/html/index.html)

[Linux Administration Made Easy, by Steve Frampton](https://tldp.org/LDP/lame/LAME/linux-admin-made-easy/)

[Securing and Optimizing Linux, by Gerhard Mourani](https://www.amazon.com/Securing-Optimizing-Linux-Hacking-Solution/dp/0968879314)

[Practical Guide to Linux Commands, Editors, and Shell Programming, A 4th Edition](https://www.amazon.com/Practical-Guide-Commands-Editors-Programming/dp/0134774604/ref=sr_1_1)

[UNIX and Linux System Administration Handbook, 4th edition by Evi Nemeth, Garth Snyder, Trent R. Hein and Ben Whalel](https://www.amazon.com/UNIX-Linux-System-Administration-Handbook/dp/0134277554)

[The Practice of System and Network Administration, 2nd edition by Thomas A. Limoncelli, Christina J. Hogan, and Strata R. Chalup](https://www.amazon.com/Practice-System-Network-Administration-Enterprise/dp/0321919165/ref=sr_1_1)

### Ubuntu

[Ubuntu](https://www.ubuntu.com/)

[Ubuntu Help](https://help.ubuntu.com/)

[Ubuntu Forums](https://www.ubuntuforums.org/)

[Ask Ubuntu](https://askubuntu.com/)

[Ubuntu Tutorials](https://tutorials.ubuntu.com/)

[Ubuntu Community](https://community.ubuntu.com/)

### Internet Relay Chat

[8 Best IRC Clients for Linux in 2024](https://www.tecmint.com/best-irc-clients-for-linux/)

Channels

* #linux
* #linuxhelp

## Chapter 3: Working with GNOME

[Wayland](https://wayland.freedesktop.org)

### Using X

The /usr directory and its subdirectories contain the majority of the Xorg software.
Some important subdirectories are as follows:

* /usr/bin
* /usr/include
* /usr/lib
* /usr/lib/X11
* /usr/lib/modules

```
find /usr -name xorg.conf
/usr/share/doc/xserver-xorg-video-intel/xorg.conf
```

### References

[GNOME](https://www.gnome.org)

## Chapter 4: On the Internet

### Choosing an Email Client

* Mozilla Thunderbird
* Evolution - Email, Contacts and Calendars

### Internet Relay Chat

#### IRC Clients

* XChat
* Pidgin
* Quassel
* HexChat

Console Clients

* epic
* irssi

### Usenet Newsgroups

### References

* [www.mozilla.com](https://www.mozilla.com/) -- The home page for Mozilla Firefox and Thunderbird
* [A history of Usenet](http://en.wikipedia.org/wiki/Usenet)

## Chapter 5: Productivity Applications

### Introducing LibreOffice

* Writer - Word Processing
* Calc - Spreadsheet
* Impress - Presentations

All but Dia are part of the LibreOffice project:

* Math - Math Formula Editor
* Base - Database application
* Draw - Graphics application
* Dia - Technical Drawing Editor
* Planner - Project Management

Competitive Productivity Application Suites

* Oracle - Open Office
* IBM - Lotus Symphony
* LibreOffice

### Working with PDFs

Reading a PDF in Ubuntu is available by default. It opens in Evince.

You can also install Adobe Reader from the Ubuntu Software Center from the Canonical Partners section.

pdfedit is available.

### Working with XML and DocBook

* gedit - called Text Editor in the Dash
* Publican - publication system for DocBook
* [XML Copy Editor](http://xml-copy-editor.sourceforge.net/) - Designed for most markup languages

### Working with LaTex

Some LaTex editors are availble from the Ubuntu Software Center.

* [Texmaker](http:www.xm1math.net/texmaker/)
* [LyX](http://www.lyx.org/)
* [Kile](http://kile.sourceforge.net)

### Productivity Applications Written for Microsoft Windows

Some Microsoft Windows applications can be installed and run in Linux 
using [Wine](https://appdb.winehq.org/).

### References

* [LibreOffice](http://www.libreoffice.org/)
* [Document Foundation](http://www.documentfoundation.org/)
* [Open Office](http://www.openoffice.org)
* [PDF Edit](http://www.pdfedit.cz/en/index.html)
* [CodeWeavers CrossOver Office](http://www.codeweavers.com/) Enables some Windows programs to run under Linux.

## Chapter 6: Multimedia Applications

### Sound Cards

* [ALSA](http://alsa-project.org/main/index.php/Main_Page) - *Advanced Linux Sound Architecture*
* OSS - *Open Sound System*

### Adjusting Volume

Click the speaker icon in the top-right corner of the screen and move slider left or right.

Alteratively: Settings: Sound tab

### Sound Formats

* RAW (.raw) - *headerless format*
* MP3 (.mp3)
* WAV (.wav) - Uncompressed Windows audiovisual sound format
* OGG Vorbis (.ogg) - Ubuntu's preferred audio encoding format.
* FLAC (.flac) - *Free Lossless Audio Format*

For MP3, download a plugin for GStreamer.
Install the gstreamer0.10-plugins-ugly package, which enables the MP3 codec in all the
GNOME applications.

To convert between sound formats, use the *sox* command.

### Listening to Music

#### Rhythmbox

Plays audio CDs. Can copy music to your computer.

[Ubuntu Podcast](http://ubuntupodcast.org/)

#### Banshee

Another music application that can rip and play back music.

### Graphics Manipulation

Installed by default: [Shotwell Photo Manager](https://shotwell-project.org/doc/html/index.html)

#### The GNU Image Manipulation Program (GIMP)

GIMP is free, but not installed by default.

#### Using Scanners in Ubuntu

Simple Scan is installed by default.

#### Working with Graphics Formats

* BMP (.bmp) - Bitmapped graphics, typically used in Microsoft Windows
* GIF (.gif) - CompuServe Graphics Interchange Format
* JPG (.jpg) - Joint Photographic Experts Group
* PCX (.pcx) - IBM Paintbrush
* PNG (.png) - Portable Network Graphics
* SVG (.svg) - Scalable Vector Graphics
* TIF (.tif) - Tagged Image File Format

*convert* utility from ImageMagick, *netpbm* family of utilities
```
convert image.gif image.png
```

* ppm - portable pixmap file format
* pgm - portable graymap file format
* pnm - portable anymap file format
* pbm - portable bitmap file format

#### Capturing Screen Images

Search Activities for screenshot

Search Activities for paint

#### Other Graphics Manipulation Options

* [Blender](http://www.blender.org/) - 3-D image and animation editor
* [CinePaint](http://www.cinepaint.org/) - A powerful and complex tool used by Hollywood studios
* [darktable](http://www.darktable.org) - A RAW editor
* [digiKam](http://www.digikam.org/) - Photo management software
* [Hugin](http://hugin.sourceforge.net/) - Panoramic photo stitcher
* [Inkscape](http://inkscape.org/) - SVG - Vector Graphics creation and editing tool
* [POV-Ray](http://www.povray.org/)
* [Radiance](http://www.radiance-online.org/)
* [Xara Xtreme](http://www.xaraxtreme.org) - A general purpose graphics editor

#### Using Digital Cameras with Ubuntu

##### Handheld Digital Cameras

##### Using Shotwell Photo Manager

[Shotwell Photo Manager](https://shotwell-project.org/doc/html/index.html)

### Burning CDs and DVDs in Ubuntu

Learning how to burn discs is essential if you have to download and install a Linux distribution

*Ripping* refers to extracting music tracks from a music CD.

#### Creating CDs and DVDs with Brasero

Brasero is a graphical client.
It also creates ISO files, which are disc images that contain everything that would exist on the medium if you burned a real CD or DVD in one file that can be mounted by computer file systems.

#### Creating CDs from the Command Line

use the *mkisofs* command to create the ISO image.

```
mkisofs -r -v -J -1 -o /tmp/our_special_cd.iso /source_directory
```
* -r - sets the permissions
* -v - displays verbose messages
* -J - uses the Joliet extensions to ISO9660 so that Windows can read the CD
* -1 - allows 31 character filenames; DOS does not like it, but everyone else does
* -o - defines the directory where the image will be written
* /source_directory - indicates the path to the source directory

```
cdrecord -eject -v speed-12 dev=0,0,0 /tmp/our_special_cd.iso
```

* -eject - Ejects the CD when the write operation is finished
* -v - Displays verbose messages
* speed= - Sets the speed, depends on drive
* dev= - Specifies the device number of the CD writer

You can also use the blank=option with the *cdrecord* command to erase CD-RW discs

Current capacity for CD media is 7000MB of data or 80 minutes of music.

#### Creating DVDs from the Command Line

DVD Formats:

* DVD+R
* DVD-R
* DVD+RW
* DVD-RW

You need to have the dvd+rw-tools package installed, as well as the cdrtools package.
The dvd+rw-tools package contains the growisofs applicatin (which acts as a front end
to *mkisofs*) and the DVD formatting utility.

1. Format the disc with dvd+rw-format /dev/scd0, where /dev/scdo is the device name for your drive.
2. Write your data to the disc with growisofs -Z /dev/scd0 -R -J /your_files

Caution: 
Some DVDs come pre-formatted: formatting them again makes them useless.

### Viewing Video

#### TV and Video Hardware

Install a TV Card

[Current list of TV and video cards supported in Linux](http://linuxtv.org/index.php/Main_page)

To determine what chipset yoru TV card has:

```
lspci
```

#### Video Formats

* AVI (.avi) - The Windows audiovisual format
* FLV (.flv) - Used in Adobe Flash
* MPEG (.mpeg) - The MPEG video format, also known as .mpg
* MOV (.mov) - A QuickTime video format
* OGV/OGG (.ogv/.ogg) - The Ogg Theora freely licensed video format
* QT (.qt) - The QuickTime video format from Apple
* WEBM (.webm) - Google's royalty-free container for audio and video, designed for HTML5

#### Viewing Video in Linux

Install the ubuntu-restricted-extras package from the Ubuntu software repositories.

You can watch video files and video DVDs with the Totem Movie Player, which is installed by default.

Another interesting video viewer application is VLC, which is available in the software repositories and also for other operating systems.

#### Personal Video Recorders

The best reason to attach a television recorder antenna to your computer is to use the video card
and the computer as a personal video recorder.

The commercial personalvideo recorder TiVo started a new trend by using Linux running on a PowerPC  
processor to record television programming witha variety of customizations.

#### Video Editing

You can now create and edit video in Ubuntu by using PiTiVi. Searchfor: "PiTiVi video editor" in the
Ubuntu Software Center.

#### References

* [VLC - VideoLan](http://www.videolan.org/) - A multimedia player project that will play almost anything
* [HOWTO for creating DVDs under Linux](http://fy.chalmers.se/~appro/linux/DVD+RW/)
* [gimp](http://www.gimp.org/)
* [SANE - Scanner Access Now Easy](http://www.sane-project.org/)
* [ImageMagick](http://www.imagemagick.org)
* [GIMP Tutorials](http://gimp.net/tutorials/)

## Chapter 7: Other Ubuntu Interfaces

### Desktop Environment

#### KDE and Kubuntu

#### Xfce and Xubuntu

#### LXDE and Lubuntu

#### MATE and Ubuntu MATE

#### Ubuntu Budgie

[Ubuntu Budgie Desktop](https://ubuntubudgie.org/)

#### Ubuntu Kylin

Ubuntu Kylin is Ubuntu localized for China.

#### References

[Metacity blog](http://blogs.gnome.org/metacity/2007/12/23/start-reading-here/) “Many window managers are like Marshmallow Froot Loops; Metacity is like Cheerios.”

[Compiz](http://www.compiz.org/) Web site unavailable?

[Enlightenment](http://www.enlightenment.org/)

[KDE Desktop](http://www.kde.org/)

[Kubuntu](http://www.kubuntu.org/)

[Xfce](http://www.xfce.org/)

[xubuntu](http://www.xubuntu.org/)

[LXDE](https://www.lxde.org/) 

[Lubuntu](http://lubuntu.net/)

[GNOME](http://www.gnome.org/)

[Ubuntu Budgie](http://ubuntubudgie.org/)

[Ubuntu MATE](http://ubuntu-mate.org/)

[Ubuntu Kylin](https://wiki.ubuntu.com/UbuntuKylin) The English language resource for Ubuntu Kylin

[Ubuntu Derivatives](http://www.ubuntu.com/project/about-ubuntu/derivatives)

[Live CD/DVD Linux distribution, Knoppix](http://www.knoppix.net/)

[Desktop Envionment Wiki (General)](http://en.wikipedia.org/wiki/Desktop_environment)

[Comparison of X Window System desktop environments wiki](http://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments)

## Chapter 8: Games

### Ubuntu Gaming

Emulators enable you to play classic games.

There are emulators for DOS, NES, SNES, and many more platforms.

* DGen/SDL
* DOSBox
* xtrs
* FCE Ultra
* GnGeo
* SDLMame
* ScummVM
* Stella

### Installing Proprietary Video Drivers

Open Software & Updates and select the Additional Drivers tab.

### Online Game Sources

#### [Steam](http://steampowered.com/)

Steam is a cross-platform entertainment platform.

Steam is created by Valve Software, usually referred toas just "Valve".

[Valve and Steam](http://store.steampowered.com/)

#### [GOG.com](https://www.gog.com/games)

#### [Humble](https://www.humblebundle.com/store)

#### [Itch.io](https://itch.io/games)

#### [LGDB - Linux Game Database](https://lgdb.org/games)

https://www.protondb.com/

https://www.gamingonlinux.com/itemdb.php

#### [Game Jolt](https://gamejolt.com/games/best?os=linux)

### Installing Games in Ubuntu

* Warsow
* Scorched 3D
* Frozen Bubble
* SuperTux
* [Battle for Wesnoth](http://wesnoth.org/)
* Frets on Fire
* FlightGear
* Speed Dreams
* Games for Kids
* Commercial Games

#### Playing Windows Games

*Wine* runs a large number of Windows programs, including many games.

#### References

* [Warsow](http://www.warsow.net/)
* [Scorched 3D](http://www.scorched3d.co.uk/)
* [Frozen Bubble](http://www.frozen-bubble.org/) Obsolete?
* [SuperTux](http://supertux.lethargik.org/)
* [Battle for Wesnoth](http://wesnoth.org/)
* [gCompris](http://gcompris.net/) Children's games?
* [Frets on Fire](http://fretsonfire.sourceforge.net)
* [Childsplay](http://childsplay.sourceforge.net/)
* [Tux Paint](http://www.tuxpaint.org/)
* [FlightGear](http://www.flightgear.org/)
* [Speed Dreams](http://www.speed-dreams.org/)
* [Games on Ubuntu](https://help.ubuntu.com/community/Games)
* [NVIDIA Unix/Linux drivers](http://www.nvidia.com/object/unix.html)
* [Wine - Wine Is Not an Emulator](http://help.ubuntu.com/community/Wine)
* [Wine HQ](http://www.winehq.org/)

## Chapter 9: Managing Software

### Ubuntu Software

```
gnome-software
```

### Using Synaptic for Software Management

If you need to install something specific -- such as a library -- you need to use Synaptic.

You can install Synaptic by using Ubuntu Software.

#### Day to Day Usage

```sudo apt-get update && sudo apt-get upgrade```

#### Sample install of MySQL 

```sudo apt-get install mysql-sever mailx```

#### Finding Software

```apt-cache search kde```

Search only in package names, not in their descriptions by using the -n parameter

```apt-cache -n search kde```

#### Using apt instead of apt-get

There is a new simplified to APT that removes the hyphen and the second part of the command.
It also includes lovely updates like a progress bar.

### Compiling Software from Source

Two ways you to do it:

* Use the source code available in Ubuntu repositories
* Use the source code provided by upstream developers

For either method, you need to install the `build-essential` package to ensure
you have the tools you need for compilation. You may also need to install 
`automake` and `checkinstall`, which are build tools.

#### Compiling from a Tarball

```
tar zxvf packagename.tgz -C ~/source
tar zxvf packagename.tar.gz -C ~/source
tar zxvf packagename.bz -C ~/source
tar zxvf packagename.tar.bz2 -C ~/source
```

If you are not certain what file compression method was used, use the file command
to figure it out:

```file packagename```

Change directories to ~/source/packagename and look for a file named README, INSTALL, or
something similar. 

Typically, the procedure to compile source code is as follows:

```./configure```

```make```

```sudo make install```

In case of error, run `make clean` beforee trying again.

You may also need to remove the software: `sudo make uninstall`

#### Compiling from Source from the Ubuntu Repositories

First, get the source from the Ubuntu repositories:

```apt-get source foo```

Install the build dependencies:

```sudo apt-get build-dep foo```

```cd foo-4.5.2```

Next, create a new debian/changelog entry. Enter a message that ells why a new version was 
made, perhaps something like Matthew's flight of fancy with extra sauce.

`dch -i`

### Configuration Management

#### dotdee

If you run Linux-based systems, you will find a series of directories that end with a .d and that store configuration files. These are sometimes called .d or "dot dee" directories.

### Ubuntu Core

### Using Snaps

Software bundles that can be packaged using Ubuntu Core are called snaps. Snaps can be 
installed using Ubuntu Software or from the command line.


```
snap find
snap find searchterm
# To install a snap package
sudo snap install packagename
snap list
sudo snap refresh packagename
snap changes
```

### References

* [History of the Debian Linux package system](https://www.debian.org/manuals/project-history/ch-detailed.en.html)

* [Synaptic package manager](http://www.nongnu.org/synaptic/)

## Chapter 10: Command-Line Beginner's Class

### What is the Command Line?

### Accessing the Command Line

To start a terminal window (from the command line):

```gnome-terminal```

Doesn't work: `Ctrl-Alt-F1` starts a command line window.
2-6 might work.

Ctrl-Alt-F7 does't return to a graphical interface.

Another way, just press Alt + right or left arrow couple times, until you get out of gui. 
Ubuntu by default has like 6 black screens (ttys), and 7th is the gui 

### Text-Based Console Login

Type user name and password when prompted.

Print Working Directory (pwd)

#### Logging Out

Use the `exit` or `logout` command or press `Ctrl-D` to end your session.

#### Logging In and Out from a Remote Computer

The ssh client features many command-line options but can simply be used 
with the name or IP address of the remote computer:

`ssh 192.168.0.41`

### User Accounts

To use super user privileges from the command line, you need to preface the command 
you want to execute with another command, `sudo` (super user do), followed by a space and the command 
you want to run. You will then be prompted by the password.

In Ubuntu, the root account is disabled by default because forcing users with super user privileges
to type a specific command every thime they want to execute a command as a super user 
should have the benefit of making them carefully consider what they are doing when they
use that power.

However, if you are more experienced and comfortable with the more traditional method of
using super user privileges and want to enable the root account, you can use the command
`sudo passwd`.

An alternative way of getting a root prompt, without having to enable the root account,
is to issue the command `sudo -i`. After entering your password, you find yourself at a
root prompt (#). Do what you need to do, and when you are finished type exit and press 
Enter to return to your usual prompt.

[sudo and root](https://help.ubuntu.com/community/RootSudo)

### Reading Documentation

#### Using Man Pages

Man pages are stored in places like `/usr/share/man` and `/usr/local/share/man`, but
you don't need to know that.

Use the man command like this:

`man rm`

`info info`

#### Using `apropos`

`apropos partition`

#### Using `whereis`

To find a command and its documentation, you can use the `whereis` command.

`whereis fdisk

### Understanding the Linux File System

Man page for the Linux file system hierarchy:

`man hier`

#### Essential Commands in `/bin` and `/sbin`

#### Configuration Files in /etc

* fastab - The file system table
* modprobe.d - instructions to load kernel modules
* passwd - This file holds the list of users for the system
* sudoers - This file holds a list of users or user groups with super user access

#### User Directories: /home

#### Using the Contents of the `/proc` Directory to Interace with the Kernel

The contents of the `/proc` directory are created from memory and exist only while
Linux is running.

`free`

`cat /proc/meminfo`

#### Working with Shared Data in the `/usr/` Directory

#### Temporary File Storage in the `/tmp` Directory

Used for Temporary File Storage

#### Accessing Variable Data Files in the `/var` Directory

The `/var` directory contains subdirectories used by various system services for spooling and logging.

Also used for FTP.

### Navigating the Linux File System

#### Listing the Contents of a Directory with `ls`

`ls`

You can see all the hidden files by adding the "-a" command line option.

`ls -a`

`ls -al`

Recursively view directories and sub-directories

`ls -R`

`ls -laR > listing.txt`

#### Changing Directories with `cd`

`cd somedir`

`cd /home/matthew/stuff/somedir`

`cd ..`

`cd $HOME`

`cd ~`

#### Finding Your Current Directory with `pwd`

`pwd`

### Working with Permissions

```
$ touch file
$ ls -l file
-rw-rw-r-- 1 dstevenson dstevenson 0 Dec 10 12:12 file
```

* The type of file created
* Permissions
* Number of links to the file
* The owner
* The group
* file size and creation/modification date

#### Assigning Permissions

In Linux, permissiosn are grouped by owner, group and others, with read, write, and execute permission assigned to each (rwx).

* `r` indicates permission to open and read a file
* `w` indicates permission to open and write to a file
* `x` indicates permission to execute a file (or read a directory)

Numeric codes:

* 4 indicates read permission
* 2 indicates write permission
* 1 indicates execute permission

Defined groups are maintained by the `root` operator , but you can use the `newgrp` command to temporarily join other groups to access files (as long as the root operator has added you to the other groups).

You can also allo or deny other groups' access to your files by modifying the group permissions of your files.

```
$ groups
dstevenson adm cdrom sudo dip plugdev lpadmin sambashare
```

```
$ whoami
dstevenson
```

#### Directory Permissions

```
$ mkdir directory
$ ls -ld directory
drwxrwxr-x 2 dstevenson dstevenson 4096 Dec 10 12:20 directory
```

If you examine a device file for a Linux serial port, you see the following:

```
$ ls -l /dev/ttyS0
crw-rw---- 1 root dialout 4, 64 Dec 10 11:30 /dev/ttyS0
```

`c` designates a serial communications port.

```
$ ls -l /dev/sda
brw-rw---- 1 root disk 8, 0 Dec 10 11:30 /dev/sda
```

`b` designates a block device.

#### Altering File Permissiosn with `chmod`

This command using various forms of command syntax, including octal or a mnemonic form (such as u, go, o, or a and rwx, and so on).
* u - user
* g - group
* o - others
* a - all
* r - read permission
* w - write permission
* x - execute permission

You can use the `chmod` command to add,remove or modify file or directory permissions.

When you createa file, it uses the default permissions (set by `umask` in /etc/bashrc).

Remove write permissions for everyone:

```
$ ll readme.txt
-rw-rw-r-- 1 dstevenson dstevenson 0 Dec 10 12:29 readme.txt
$ chmod a-w readme.txt
$ ll readme.txt
-r--r--r-- 1 dstevenson dstevenson 0 Dec 10 12:29 readme.txt
```

```
$ ll readme.txt
-r--r--r-- 1 dstevenson dstevenson 0 Dec 10 12:29 readme.txt
$ chmod u+rw readme.txt
$ ll readme.txt
-rw-r--r-- 1 dstevenson dstevenson 0 Dec 10 12:29 readme.txt
```

#### File Permissiosn with `umask`

The numbers we used above when discussing file permissions are also used with `umask`.

Now, the numbers defined in `umask` are subtracted from the ultimate file permissions (777).

If you wanted all new files created with a default permission of 777, you would type this.

```$ umask 000```

#### File Permissions with `chgrp`

```chgrp wheel filename```

#### Changing file Permissiosn with `chown`

```chown dstevenson filename```

You can also use the chown command to change the group of the file at the same time:

```chown destevenson:wheel filename```

#### Understanding Set User ID, Set Group ID, and Sticky Bit Permissions

One commonly used program with suid (set user id) permissions is the passwd command:

```
$ ls -l /usr/bin/passwd
-rwsr-xr-x 1 root root 68208 Feb  6  2024 /usr/bin/passwd
```

This setting allows normal users to execute thecommand (as root) to make changes to a root-only-accessible file (/etc/passwd).

By defaul,t suid and sgid are turned off on files. To set them, add an extra digit to the beginning of a number in a `chmod` command. `Suid` uses `4`. `Sgid` uses `2`.

```
$ chmod 4711 filename
```

Savvy Linux system administrators keep the number suid or sgid files present on a system to a minimum.

```
sudo find / -type f -perm /6000 -exec ls -l {} \;
```

A sticky bit limits who many rename or delete files within a directory. 
When it is set, files in that directory may be unlinked or renamed only 
by a super user, the directory owner, or the file owner.

```chmod 1755 directoryname```

#### Setting Permissions with Access Control Lists

```
$ getfacl readme.txt
# file: readme.txt
# owner: dstevenson
# group: dstevenson
user::rw-
group::r--
other::r--
```

You can add multiple users and groups with permissions specific to each.

```setfacl -m u:sanda:rwx readme.txt```

Remove and reset `sandra`'s permissions on the file:

```setfacl -r u:sandra: readme.txt```

-m is for modify and -r is for remove.

```
setfacl -m g:groupname:rwx secrets.txt
setfacl -m o:r secrets.txt
```
A useful feature is masking, which allows you to list only the permissions that are available:

`setfacl -m m:rx readme.txt`

### Working with Files

#### Creating a File with `touch`

```
touch myfile
touch randomdirectory/newfile
touch /home/dstevenson/randomdirectory/newfile
touch `/randomdirectory/newfile
```

#### Creating a Directory with `mkdir`

```
mkdir newdirectory
mkdir music/newdirectory
mkdir /home/destevenson/music/newdirectory
mkdir ~/music/newdirectory

# Create all subdirectories

mkdir -p ~/music/newdirectory/subdir1/subdir2
```

#### Deleting a Directory with `rmdir`

```
rmdir directoryname
rmdir music/directoryname
rmdir /home/matthew/music/directoryname
rmdir ~/music/directoryname
```

#### Deleting a File with `rm`

```
rm filename
rm randomdirectory/filename
rm /home/matthew/randomdirectory/filename
rm ~/randomdirectory/filename

# Delete a directory and all its contents
rm -r /home/matthew/randomdirectory
```

#### Moving or Renaming a File with `mv`

````
mv documents/filename archive
mv oldfilename newfilename
mv documents/oldfilename archive/newfilename
mv /home/matthew/documents/oldfilename /home/matthew/archive/newfilename
mv ~/documents/oldfilename ~/archive/newfilename
````

#### Copying a File with `cp`

```
cp documents/filename archive
cp oldfilename newfilename
cp documents/oldfilename archive/newfilename
cp /home/matthew/documents/oldfilename /home/matthew/archive/newfilename
```

#### Displaying the contents of a file with `cat`

```
cat filename
```

#### Displaying the contents of a File with `less`

```
less filename
```

`more` does not give the ability to scroll up and down


#### Using Wildcards and Regular Expressions

`rm abc*`

### Working as Root

```
sudo command with command line parameters
```

**Caution:** Before editing any important system or software service configuration file, make a backup copy.

#### Understanding and Fixing `sudo`

In order for a user to use `sudo`, the user account must belong to the *sudo* group and must also be listed in the `/etc/sudoers` file.

##### Recovery Mode - Getting Root Access Again

1. Hold the Shift key down while the computer is booting.

2. When the GRUB menu page appears, use the arrow key on your keyboard to scroll to the
entry that ends with (recovery mode) and press Enter to select it

3. When the boot process finishes, and you have several options, select the menu entry for rot: Drop to Root Shell Prompt.

4. Because Ubuntu mounts file systems as read-only by default in recovery mode, 
you need to remout the root file system, /, as read/write so that you can fix the problem.

```
# mount -o rw,remount
```

if the problem exists because the user account was removed from the admin group, enter the following:

```
# aduser username admin
```

If the problem exists because the permissiosn for `/etc/sudoers` are wrong, enter this:

```
# chmod 440 /etc/sudoers
```

If the problem exists because of an internal problem in `/etc/sudoers`, make a backup of the existing file and use `visudo` to edit.

After your fix is complete, enter the root command line:

`# exit`

#### Creating Users

When a Linux system administrator creates a user, an entry is created in  `/etc/passwd` for the user. The system also creates a directory, labeled with the user's user name, in the `/home` directory.

```
sudo adduser sandra
sudo passwd sandra
```

#### Deleting Users

```
sudo deluser --remove-all-files -remove-home sandra
```

#### Shutting Down the System

```
$ sudo shutdown -h now
$ sudo shutdown -h 0
$ sudo shutdown -h 18:30 "System is going down for maintenance this evening at 6:30 pm. Please make sure you have saved your work and logged out by then or you may lose data"
```

#### Rebooting the System

```
sudo shutdown -r now
sudo shutdown -r 0
```

Other commands you can use to shut down and reboot Linux are the `halt` and `reboot` commands, but the `shutdown` command is more flexible.

### Commonly Used Commands and Programs

* Managing users and groups - cvhage, chfn, chsh, edquota, gpasswd, groupadd, groupdel, groupmod, groups, mkpasswd, newgrp, newusers, passwd, umask, useradd, userdel, usermod
* Managing files and file systems - cat, cd, chattr, chmod, chown, compress, cp, dd, fdisk, find, gzip, ln, mkdir, mksfs, mount, mv, rm, rmdir, rpm, sort, swapon, swapoff, tar, touch, umount, uncompress, uniq, unzip, zip
* Managing running programs, bg, fg, kill, killall, nice, ps, pstree, renice, top, watch
* Getting information - apropos, cal, cat, cmp, date, diff, df, dir, dmesg, du, env, file, free, grep, head, info, last, less, locate, ls, lsattr, man, more, pinfo, ps, pwd, stat, strings, tac, tail, top, uname, uptime, vdir, vmstat, w, wc, whatis, whereis, which, who, whoami
* Console text editors, ed, jed, joe, mcedit, nano, red, sed, vim
* Console, Internet and network commands - bing, elm, ftp, host, hostname, ifconfig, links, lynx, mail, mutt, ncftp, netconfig, netstat, pin, ping, pump, rdate, route, scp, sftp, ssh, tcpdump, traceroute, whois, wire-test

See man page for more information.

### References

* [The Ubuntu community help page for using the terminal](https://help.ubuntu.com/community/UsingTheTerminal)
* [Overview of the Linux file system tree](https://help.ubuntu.com/community/LinuxFilesystemTreeOverview)
* [`sudo` - philosophy behind using it by default, and how to use it](https://help.ubuntu.com/community/RootSudo)