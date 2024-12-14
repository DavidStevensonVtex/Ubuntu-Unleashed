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