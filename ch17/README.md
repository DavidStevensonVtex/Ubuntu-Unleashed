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
