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