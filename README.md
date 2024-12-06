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

