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

