# Ubuntu Unleashed, 2019 Edition

## Chapter 15: The Boot Process

### Running Services at Boot

Known as runlevels, they defien what system services are started upon boot.

These services are simply applications running in the background that provide some needed function to a system, such as gettign information from the mouse and sending it to the display; or a service could monitor the partitions to see whether they have enough free space left on them.

Services are typically loaded and run (also referred to as being started) during the boot process, in the same way as Microsoft Windows services are.

Starging in 2015, Ubuntu switch to another system systemd.

3 init systems:
* sysvinit - old outdated, and allows for a sequential startup of services.
* upstart
* systemd

Both upstart and systemd are designed to tackle the limitations of init, and allows for concurrent service initialization, that is, multiple services can startup at the same time, as long as they are not dependent on each other.

Both Upstart and Systemd are event based.

### Beginning the Boot Loading Process

The BIOS is an application stored in a chip on the motherboard that initializes the hardware on the motherboard (and often the hardware that's attached to the motherboard). The BIOS gets the system ready to load and run the software that we recognize as the operating system.

As a last step, the BIOS code looks for a special program known as the boot loader or boot code. These instructions tell the BIOS where the Linux kernel is located, how it should be loaded into memory, and how it should be started.

If all goes well, the BIOS looks for a bootable volume such as a floppy disk, CD-ROM, hard drive, RAM disk, USB drive, or other media.

MBR - Master Boot Record

UEFI - Unified Extensible Firmware

UEFI serves a similar role to BIOS and has replaced BIOS in most modern systems.

* [UEFI](https://help.ubuntu.com/community/UEFI)

[Difference between GPT and MBR when partitioning a drive](http://www.howtogeek.com/193669/whats-the-difference-between-gpt-and-mbr-when-partitioning-a-drive/)

#### Loading the Linux Kernel

In a general sense, the kernel manages the system resources.

TRaditionally, the Linux kernel loads and runs a process named `init`, which is also known as the "ancestor of all processes" because it starts every subsequent process.

* The traditional `init` system was SysVInit. It has been replaced by newer options.
* One of these options was `Upstart`.
* Upstart was replaced by `systemd` as of Ubuntu 15.04.

To make the system useful for users, you need to start the system servies.

#### System Services and Runlevels

* The `init` command traditionally boots a Linux system to a specific system state, commonly referred to as its *runlevel*.
* Runlevels determine which of the many available system services are started, as well as which order they start.
* A special runlevel is used to stop the system, and a special runlevel is used for system maintenance.

#### Runlevel Definitions

The runlevels are defined in a traditional Linux system in `/etc/init.d`. Some distributions use the traditional `/etc/inittab` file to manage boot services. Ubuntu has not used this file for several years. This book does not cover `/etc/inittab`.

* Runlevel 0 - Known as "halt", this runlevel shuts down the system.
* Runlevel 1 - This is a special runlevel, defined as "single" which boots Ubuntu to a root access shell prompt, where only the root user may log in. It has networking, X, and multiuser access turned off. This is the maintenance or rescue mode.
* Runlevels 2-5 - These runlevels aren't used in Ubuntu in any way that distinguishes them from eachother, but they are used in other Linux distributions.
* Runlevel 6 - This runlevel reboots the system.

Never forget that uncontrolled physical access is a virtual guarantee of access to your data by an intruder.

#### Booting into the Default Runlevel

Ubuntu boots into runlevel 5 by default, which means it starts the system as normal and leaves you inside the X Window System, looking at the graphical login prompt. It knows what runlevel 5 needs to load by looking in the rc*.d directories in `/etc`. Ubuntu contains directories for rc0.d through to rc5.d and rcS.d.

`ll /etc | egrep "rc[0-9A-Za-z].d"`

The K or S in the file name prefixes indicates whether a particular service should be killed (K) or started (S) and pass a value of stop or start to the appropriate /etc/init.d script.

The files have numbers that indicate the particular order.

The files are symlinks to initialization files in the `/etc/init.d` folder.

#### Understanding `init` Scripts and the Final State of Initialization

The logic in `init` scripts may look like the following:

```
case "$1" in
    start)
        start
        ;;
    stop)
        stop
        ;;
    restart)
        restart
        ;;
    reload)
        reload
        ;;
    status)
        rhstatus
        ;;
    condrestart)
        [ -f /var/lock/sysys/smb ] && restart || : 
        ;;
    *)
        echo $"Usage: $0 {start|stop|restart|status|condrestart}"
        exit 1
esac
```

this script approach means that you do not have to halt the system in total to start, stop, upgrade, or install new services.

If you are using a runlevel other than 5, the final act of the `init` process is to launch the user shell -- `bash`, `tcsh`, `zsh`, or any many other command shells available.

#### Controlling Services at Boot with Administrative tools

You can configure what services run at startup with Startup Applications Preferences (shown in Fiture 15.1).

#### Changing Runlevels

You can use the `telinit` command to change runlevels on the fly on a running Ubuntu system.

Inthe past a system administrator could quickly change the system to maintenance or single-user mode by using the `telinit` command with its `S` option, like this:

`sudo telinit S`

Today, the same thing would be done using this `systemd` command.

`sudo systemctl rescue`

The `telinit` command uses the `init` command to  change runlevels and shut down currently running sevices. However, under `systemd`, `telinit` is deprecated.

After booting to single-user mode, you used then return to multi-user mode, like this:

`sudo telinit 2`

Today, the same thing would be done using the `systemd` command:

`systemctl default`

#### Troubleshooting Runlevel Problems

Use the following to read kernel output after booting:

`dmesg | less`

`cat /var/log/messages | less`

### Starting and Stopping Services Manually

`sudo /etc/init.d/apachee2 start`
Starting apache 2.2 web server

### Using `Upstart`

### Using `systemd`

* systemctl start servicename service - Start a service
* systemctl stop servicename service - Stop a service
* systemctl restart servicename service - Restart a service
* systemctl reload servicename service - Reload a service - rells the service to reload its configuration files
* systemctl status servicename service - Show the status of a service
* systemctl condrestart servicename service - Restart a service if it is already running
* systemctl enable servicename service - Enable a service at startup
* systemctl disable servicename service - Disable a service at startup
* systemctl - list services
* systemctl list-unit-files - show all installed unit files
* systemctl halt - halt the system
* systemctl reboot - reboot the system
* journalctl -f - Follow the system log; replaces tail -f /var/log/message

Services are defined in `systemd` unit files, which end with `.service`. Many exmples of these are found in `/lib/systemd/system`.