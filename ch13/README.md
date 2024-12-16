# Ubuntu Unleashed, 2019 Edition

## Chapter 13: Managing Users

User management and administration includes:

* allocating and manging `/home` directories
* putting in place good password policies
* applying effective security policies
* disk quotas 
* file and directory access permissions

### User Accounts

Three types of Linux users:

* super-user
* day to day user
* system user

Ubuntu uses the /etc/passwd file to store information on user accounts.

Each user /etc/passwd contains:

* User name
* an encrypted password
* User ID - UID
* Group ID - GID
* Location of the /home directory, usually /home/username
* Default shell (/bin/bash is the default for new users)

#### The Super User / Root User

There can be only one super user account (*root user*).

The root user is unique in that it has a UID Of 0 and GID of 0.

In Ubuntu, you execute a command with root, or super user, privileges
* by using the `sudo` command:

`sudo apt-get update`

You are then prompted for your password.

the root account is disabled so no one can actually log in with the username root.

A regular user...

The system user is not a person but rather an administrative account that the 
system uses during day-to-day running of various services.

for example, the user named `www-data` owns te Apache web server and all the associated files.

#### User IDs and Group IDs

The Ubuntu operating system identifies users and groups by numbers known as the *user ID (UID)* 
and *group ID (GID).

Numbers from 1 through 499 and number 65,534 are the system, sometimes called the logical users,
or pseudo-users.

Ubuntu creates a private GID for every UID of 1,000 and greater.

#### File Permissions

There are three types of permissions: read, write and execute (r, w, x). 
For any file, permissions are assigned to three categories: user, group and other.

* chgrp - Changes the group ownership of a file or directory
* chown - Changes the owner of a file or diretory
* chmod - Changes the access permissions of a file or directory

### Managing Groups

Groups can make managing users a lot easier.

Instead of having to assign individual permissiosn to every user, you can use groups to 
grant or revoke permisssions to a large number of users quickly and easily.

#### Group Listing

`$ cat /etc/group`

Finding your groups:

```
$ groups
dstevenson adm cdrom sudo dip plugdev lpadmin sambashare
```

#### Group Management Tools

* groupadd - This command creates and adds a new group
* groupdel - This command removes an existing group
* groupmod - This command creates a group name or GIDs but doesn't add or delete members from a group.
* gpasswd - This command creates a group password. Every group can have a group password and an administrator. Use the -A argument to assign a user as group administrator.
* useradd -G - The -G argument adds a user to a group during the initial user creation. 
* usermod -G - This command allows you to add a user to a group as long as the user is not logged in at the time.
* grpck - This command checks the /etc/group file for typos

Examples:

1. Add a new group with the `groupadd` command:

    `sudo group add dvdrw`

1. Change the group ownership of the device to the new group with the `chgrp` command:

    `sudo chgrp dvdrw /dev/scd0`

1. Add the approved user to the group with the `usermod` command:

    `sudo usermod -G dvdrw ryan`

1. Make user `ryan` the group administrator with the `gpasswd` so that he can add new users to the group:

    `sudo gpasswd -A ryan`

### Managing Users

A user must be created, assigned a UID, provided a `/home` diretory, provided an initial set of files
for his or her /home directory, and assigned to groups in order to use the system resources securely and
efficiently.

#### User Management Tools

* useradd - This command adds a new user account to the system.
* useradd -D This command sets the system defaults for creating the user's `/home` directory, account expiration date, default group, and command shell. See the specific options in the `useradd` man page. Used without any arguments, the `useradd` command displays the defaults for the system. The default files are in /etc/skel.
* deluser - This command removes a user's account (thereby eliminating that user's home directory and all files it contains). There is an older version of this command, `userdel`. `deluser` is preferred because it provides finer control over what is deleted.
* passwd - This command updates the authentication tokens used by the password management system.
* usermod - This command changes several user attributes. The most commonly used arguments are `-s` to change the shell and `-u` to change the UID. No changes can be made while the user is logged in or running a process.
* csh - This command changes the user's default shell. For Ubuntu, the default shell is /bin/bash, known as the Bash, or Bourne Again Shell.

to lock a user out of his or her account, use the following command:

`$sudo passwd -l username`

#### Adding New Users

`sudo useradd sandra -p c00kieZ4ME -u 1042`

The system administrator can also use the graphical interface that Ubuntu provides to add the same account as shown in the prceding command but with fewer setting options available.

#### Monitoring User Activity on the System

* `w` tells the system administrator who is logged in (who also does this?)
* `ac` provides information about the total connect time of the user, measured in hours

### Managing Passwords

#### System Password Policy

* Allowed and forbidden passwords
* Frequency of mandated password changes
* Retrieval or replacement of lost or forgotten passwords
* Password handling by users

#### The Password File 

The password file is `/etc/passwd`. The format for each line is:

```username:password:uid:gid:gecos:homedir:shell```

The gecos field is for miscellaneous information about the user, including their full name, office location, office and home phone number, and possibly a brief text note.

Note that colons separate all fields in the `/etc/passwd` file.

If an asterisk appears in the password field, the user is not allowed to log in. This feature exists so that a user can be easily disabled and (possibly) reinstated later without the need to create the user all over again.

The system administrator can either edit the file directly or use the `passwd -l` command.

Several services run as pseudo-users, usually with root permissions. Typically they are assigned a shell value of `/sbin/nologin` or `/bin/false`.

`egrep "nologin|false" /etc/passwd`

#### Shadow Passwords

It is considered a security risk to keep passwords in `/etc/passwd` because people could run a password cracking program. To avoid this risk, *shadow passwords* are used and stored in the `/etc/shadow` file.

Special versiosn of the traditional `password` and `login` programs must be used to enable shadow passwords.

`sudo cat /etc/shadow`

The fields are separated by colons:

* user's login name
* user's encrypted password for the user
* day on which the last password change occurred.
* The number of days before the password can be changed (which prevents changing a password and then back to the old password)
* The number of days after which the password must be changed.
* The number of days before the password expiration.
* The number of days after the password expires that the account is disabled.
* The number of days since January 1, 1970, that the account has been disabled.
* A reserved field that is not currently allocated to any use.

Note that password expiration dates and warnigns are disabled by default in Ubuntu.

PAM - Pluggable Authentication Modules

4 Management Groups:

* account management, 
* authentication management
* password management
* session management

Configuration files are in `/etc/pam.d`.

#### Managing Password Security for Users

#### Changing Passwords in a Batch

The super user can change passwords in a batch by using the `chpasswd` command,
which accepts input as a name/password pair per line in the following form:

`sud chpasswd username:password`

Passwords can be changed *en masse` * by redirecting a list of name and password pairs to the command.

Ubuntu also provides the `newusers` command to add users in a batch from a text file. 
This command also allows a user to be added to a group, and a new directory can be added for the user too.

### Granting System Administrator Privileges to Regular Users

#### Temporarily Changing User Identity with the `su` Command

The first scenario requires the existence of a root account, which is not enabled by default on Ubuntu systems and is not generally recommended in the Ubuntu community. However, there are times when this makes sense.

Note: A popular misconception is that the *su* command is short for super user; it really just means *substitute user*.

To enable the root account, you must enter the command `sudo passwd` at the command line and enter your password and a new root password. After this has been completed, you can `su` to root. 

We suggest you read the information at this [link](https://help.ubuntu.com/community/RootSudo) before doing so to ensure that you understand the reason the root account is not enabled by default.

Because almost all Linux file system security resolves around file permissions, it can be useful to occasionally become a different user with permission to access files belong to other users or groups or to acces special files (such as the communications port /dev/ttyS0...)

The syntax for *su* is:

`su option username arguments`

* -c, --command - pass a single command to the shell
* -m --preserve-environment - do not reset the environment variables
* -l - a fll login siulation for the substituted user, the same as specifying the dash alone

By using `su` alone, you can become root, but you keep your regular user environment.
This can be verified by using `printenv` command before and after the change.

by executing the following, you become root and inherit root's environment:

`$ su -`

By executing the following, you become that user and inherit the super user's environment.
Inheriting the environment comes from using the dash in the command.

`$ su - other_user`

When leaving an identity to return to your usual user identity, use the `exit` command.

```
$ su - root
Password:
root~#

# To return to the regular user's identity:
exit
```

#### Granting Root Privileges on Occasion: The `sudo` command

The problem is that UNIX permissiosn come with all or nothing authority.

Enter `sudo`, an application that permits the assignment of one, several,
or all the root-only system commands.

After it is configured, using `sudo` is simple.

`$ sudo command`

When the command is entered, `sudo` checks the `/etc/sudoers` file to see whether the user is authorzied to wield super user privileges; if so, sudo use is authorized for a specific amount of time.

The time allotted is 15 minutes by default in Ubuntu.

You must edit the `/etc/sudoers` file using `visudo`:

`$ sudo visudo`

If you want to give every user permission with no password requied to mount-the CD driveon the localhos, you do so as follows:

ALL localhos=NOPASSWD:/sbin/mount /dev/scd0 /mnt/cdrom /sbin/umount /mnt/cdrom