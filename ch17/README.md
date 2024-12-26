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

### The GNOME File Roller

The GNOME desktop file archiving graphical applicatin File Roller (`file-roller`) views, extracts, 
and creates archive files using `tar, gzip, bzip, compress, zip, rar, lha,` and serveral other 
compression formats.

This seems to go by the name Archive Manager in activities.

* [File Roller](https://help.ubuntu.com/community/File%20Roller)

### The KDE `ark` Archiving tool

```
Command 'ark' not found, but can be installed with:

sudo snap install ark  # version 24.08.3, or
sudo apt  install ark  # version 4:19.12.3-0ubuntu1.2

See 'snap info ark' for additional versions.
```

`ark` is integrated with the KDE desktop (as File Roller is with GNOME), so it might be a better choice if you use KDE.

### [Déjà Dup Backups](https://apps.gnome.org/DejaDup/)

### [Back In Time](https://backintime.readthedocs.io/)

Back In Time is a viable alternative to Déjà Dup for many users. It is easily availble from the Ubuntu software repositories, is stable, has a clear and easy-to-understand interface, and is actually little more than a GUI front end for well-established tools.