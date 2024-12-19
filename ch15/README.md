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
