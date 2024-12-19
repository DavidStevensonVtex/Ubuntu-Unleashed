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

