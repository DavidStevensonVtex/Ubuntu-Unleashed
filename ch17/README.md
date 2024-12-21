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