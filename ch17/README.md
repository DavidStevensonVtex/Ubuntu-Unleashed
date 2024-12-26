# Ubuntu Unleashed, 2019 Edition

## Chapter 17: Backing Up

### Choosing a Backup Strategy

#### Why Data Loss Occurs

The most frequent cause of data loss is human error.

Tip:

to make a backup of a configuration file you are about to edit, use the `cp` command:

`$ cp filename filename.original`

To restore it, use the following:

`$ cp filename.original filename`

Never edit or move the *.original file, or the original copy will be lost.

You can change the file's mode to be unwritable; then if you try to delete it, you are prevented from doign so and receive a warning.


Proper backups can help you recover from these problems with a minimum of hassle.

#### Assessing Your Backup Needs and Resources

* What data must be safeguarded?
* How often does the data change?

Backup schemes:

* Have a plan
* Follow the plan
* Practice your skills

Sound Practices

* Maintain more than one copy of critical data
* Label backups
* Store backups in a climate-controlled and secure area
* Use secure offsite storage of critical data.
* Establish a backup policy
* Keep track of who has access to your backup media
* Routinely verify backups and practice restorign data from them
* Routinely inspect backup media for defects and regularly replace them.

#### Evaluating Backup Strategies

* Home user
* Small office
* Small enterprise
* Large enterprise

Backup Levels

* 0 - Full backup
* 1 - Everything that has changed since the last backup
* 2
* 3 - Generates an incremental backup from the full backup
* 4 - Differential backup

#### Simple Strategy

If you need to backup just a few configuration files and some small data files, copy them to a USB stick, label it, and keept it somewhere s afe.

You can copy the important files to a CD-RW disc (up to 700 MB in size), or a DVD-RW disc (up to 8GB for data).

Most users have switched to using an external hard drive for backups because they are becoming less and less expensive and hold a great amount of data, or they have moved backups online.

Configuration and Data Files

* /home
* /etc

#### Full Backup on a Periodic Basis

A full backup on a periodic basis is a strategy that involves a backup of the complete file system on a weekly, bi-weekly or other periodic basis.

This backup strategy is not complicated to perform, and it can be accomplished with the swappable disk drives discussed later in this chapter.

#### Full Backups with Incremental Backusp

Another scheme involves performing a full backup of the entire system once per week, along with a daily incremental backup of only those files that have changed in the previous day, and it begins to resemble what a system administrator of a medium to large system traditionally uses.

`dump`

#### Mirroring Data or RAID Arrays

#### Making the Choice

* If the backup strategy is too complicated, it will be disregarded and fall into disuse
* The best scheme is often a combination of strategies; use what works.

### Choosing Backup Hardware and Media

#### Removable Storage Media

USB hard drives and solid-state "pen" drives have taken over the niche previously held by floppy drives.

Bot USB hard drives and solid-state drives are highly portable.

Support for these drives are very good.

A large USB external hard drive is also within the budgets of most and is the preferred option for anything more than could be held on one pen drive.

The biggest benefits of USB drives are data transfer speed and portability.

#### CD-RW and DVD+RW/-RW Drives

Each CD-RW disc can old 650MB to 700 MB of data.

DVD+RW/-RW is similar to CD-RW, but is more expensive and can store up to 8 GB of uncompressed data per disc.

#### Network Storage

#### Tape Drive Backups

#### Cloud Storage

Services such as Dropbox and Amazon's AWS and S3 offer a way to create and store backups offsite.

### Using Backup Software

* [Déjà Dup Backups](https://apps.gnome.org/DejaDup/)
* Amanda

#### [`tar`](http://www.gnu.org/software/tar/manual): The Most Basic Backup Tool

`info tar`

`sudo tar cvf etc.tar /etc`

`sudo tar cv /etc > etc.tar`

##### Creating Full and Incremental Backups with `tar`

To create fullbackup, using bzip2 compression of the entire system:

`sudo tar cjvf fullbackup.tar.bz2 /`

To perform an incremental backup, you must locate all the files that have been changed since the last backup.

`sudo find / -newer name_of_last_backup_file ! -a -type f -print`

##### Restoring Files from an Archive with `tar`

To restore a `tar` archive compressed with bzip2:

`$ sudo tar xjvf ubuntutest.tar.bz2`

To list the contents of a tar archive compressed with `bzip2`:

`$ sudo tar tjvf ubuntutest.tar.bz2`

#### The GNOME File Roller

The GNOME desktop file archiving graphical applicatin File Roller (`file-roller`) views, extracts, 
and creates archive files using `tar, gzip, bzip, compress, zip, rar, lha,` and serveral other 
compression formats.

This seems to go by the name Archive Manager in activities.

* [File Roller](https://help.ubuntu.com/community/File%20Roller)

#### The KDE `ark` Archiving tool

```
Command 'ark' not found, but can be installed with:

sudo snap install ark  # version 24.08.3, or
sudo apt  install ark  # version 4:19.12.3-0ubuntu1.2

See 'snap info ark' for additional versions.
```

`ark` is integrated with the KDE desktop (as File Roller is with GNOME), so it might be a better choice if you use KDE.

#### [Déjà Dup Backups](https://apps.gnome.org/DejaDup/)

#### [Back In Time](https://backintime.readthedocs.io/)

Back In Time is a viable alternative to Déjà Dup for many users. It is easily availble from the Ubuntu software repositories, is stable, has a clear and easy-to-understand interface, and is actually little more than a GUI front end for well-established tools.

#### [Unison](https://github.com/bcpierce00/unison)

[Unison File Synchronizer](https://www.cis.upenn.edu/~bcpierce/unison/)

#### [Amanda](http://www.amanda.org/)

Amanda is a powerful network backup application created by the University of Maryland at College Park.
Amanda is a robust backup and restore application best suited to unattended backups with an autoloading tape drive of adequate capacity.

There is no GUI for Amanda. Configuration is done with text files in `/etc/amanda`.

#### Alternative Backup Software

* `flexbackup` - use `flexbackup -help` for more information
* `afio`

### Copying Files

YOu can use the `tar, cp, rsync,` and even `cpio` commands to copy files.

`tar` is a traditional choice because older versions of `cp` did not handle symbolic links and permissions well at times, causing those attributes to be lost; `tar` handle those file attributes in a better manner.

`cp` has been improved to vix those problems, but `tar` is still more widely used. 
`rsync` is an excellent choice for mirroring sets of files, especially when done over a network.

#### Copying Files Using `tar`

`$ tar -cvf files | (cd target_directory ; tar -xpf)`

In this command, `file` is the filenames you want to include; you can use * to include the entire current directory.

* c - creates an archive
* v - specifies verbose - that is lists the files proccessed you you can see it is working
* f - specifies the filename of the archive. (In this case, it is -)


* x - Extract
* p - Set permissions of extracted files to those recorded in the archive
* f - Use archive file or device ARCHIVE.  If this option is not given, tar will first examine the environment variable `TAPE'.  If it is set, its value will be used as the archive name.  Otherwise, tar will assume the compiled-in default.

The following `tar` command options can be useful for creating file copies for backup purposes:

* l - Stay in the local file system (so that you do not include remove volumes)
* atime-preserve - Do not change access times on the files, even though you are accessing them now

#### Compressing, Encrypting, and Sending `tar` Streams

`$ tar -cvzf data_folder | ssh remote_host '( cd ~/mybackup_dir; tar -xvzf )'`

#### Copy Files Using `cp`

`$ cp -a source_diretory target_directory`

The `-a` argument is the same as `-dpR`:

* -d - Preserves symbolic links (by not dereferencing them) and copies the files that they point to instead of copying the links.
* -p - Presserves all file attributes, if possible. (File ownership might interfere)
* -R - Copies diretories recursively

You can also use the`cp` command to quickly replicate directories and retain permissiosn by using it with the `-avR` command line-options.

`$ sudo cp -avR directory_to_backup destination_vol_or_dir 1 > /root/backup_log.txt`

`$ sudo cp -avR ubuntu /test2 1 > /root/backup_log.txt`

This example makes an exact copy of the directory named `/ubuntu` on the volume named /test2 and saves a backup report named `backup_log.txt` under `/root`.

#### Copying Files Using `mc`

The Midnight Commander `mc` is a command-line file manager that is useful for copying, moving, and archiving files and directories.

The Midnight Commander looks and feels similr to the Norton Commander of DOS fame.

#### Using `rsync`

An old favorite for backing up is `rsync`. One big reason for this is that `rsync` enables you to copy only files that have changed since the last backup. With this tool, although the initial backup might take a long time, subsequent backups are much faster. `rsync` is also highly configurable and can be used with removable media such as USB hard drives or over a network.

First, create an empty file and call it backup.sh:

`$ sudo touch backup.sh`

```
rsync --force --ignore-errors --delete --delete-excluded --exclude-from=/home/matthew-exclude.txt --backup --backup-dir=`date +%Y-%m-%d` -av / /media/externaldrive/backup/Seymour
```

`$ sudo chmod +x backup.sh`

To restore:

`$ rsync --force --ignore-errors --delete --delete-excluded /media/externaldrive/backup/seymour`

### Version Control for Configuration Files

For safety and ease of recovery when configuration files are corrupted or incorrectly edited, the use of a version control system is recommended. In fact, this is considered industry best practice.

Version control systems are designed to make it easy to revert changes made to a file, even after the file has been saved.

`etckeeper` takes all of your `/etc/ directory and stores the configuration files from it in a version control system repository. You can configure the program by editing the etckeeper.conf file to store data in a Git, Mercurial, Bazaar, or Subversion repository.

By default, etckeeper uses Git.

First, edit /etc/etckeeper/etckeeper.conf to use your desired settingsm such as the version control system to use, the system package manager being used, and whether to have changes automatically committed daily.

`$ etckeeper init`

`$ etckeeper commit "Changed prompt style"`

You can roll a change back to the original version:

`$ bzr log /etc/bash.bashrc`

`$bzr revert =-revision 2 /etc/bash.bashrc`

### System Rescue

#### The Ubuntu Rescue Disc

The Ubuntu installation DVD (or an installation USB drive) works quite well as a live DVD.
To use it, insert the disc and reboot the computer, booting from the DVD just you did when you installed Ubuntu originally and ran it from the DVD.

#### Restoring the GRUB2 Boot Loader

The easiest way to restore a broken system's GRUB2 files is simply to replace them. Your best bet is to use installation media from the same release as what you have isntalled on the hard drive.

To get started, boot using the live DVD and open a terminal. Then determine which of the hard drive's partitions holds the Ubuntu installation, which you can discover by using the following:

`$ sudo fdisk -l`

`$ sudo fdisk /dev/sdb`

`$ sudo blkid`

`$ man fstab`

```
FSTAB(5)                                                                    File Formats                                                                   FSTAB(5)

NAME
       fstab - static information about the filesystems

SYNOPSIS
       /etc/fstab

DESCRIPTION
       The file fstab contains descriptive information about the filesystems the system can mount.  fstab is only read by programs, and not written; it is the duty
       of the system administrator to properly create and maintain this file.  The order of records in fstab is important because fsck(8), mount(8), and  umount(8)
       sequentially iterate through fstab doing their thing.
```

`$ sudo mount /dev/sda1 /mnt`

This mounts the drive in the current file system (running from the live DVD) at `/mnt`, where it will be accessible to you for reading and modifying as needed. Next, you reinstall GROUP2 on this device.

`$ sudo grub-install --boot-directory=/mnt/boot /dev/sda`

At this point, reboot (using your harddrive and not the live DVD), and all should be well.
After the reboot is complete, enter the following:

`$ sudo update-grub`

This refreshes the GRUB2 menuand completes the restoration. You can find a lot of great information about GRUB2:

* [GRUB2](https://help.ubuntu.com/community/Grub2)\

#### Saving Files from a Nonbooting Hard Drive

If restoring the GRUB2 boot loader fails and you still cannot boot from the hard drive, try to use the live DVD to recover you data. Boot and mount the hard drive qas shown previously and then attach an external st orage device such as a USB thumb drive or an external hard drive. Then copy the files you want to save from the mounted drive to the external drive.

If you cannot mount the drive at all, you options become more limited and possibly more expensive.

Every experienced system administrator has had a drive fail; no hardware is infallible. We expect occasional hardware failures, and that's why we have a good backup and recovery schemes in place for data.

There are two types of system administrators: those who lose data when this happens and those who have good schemes in place. Be forewarned and be wise.

### References

* [Backup Your System](https://help.ubuntu.com/community/BackupYourSystem)
* [Linux Documentation Project](http://www.tldp.org/)