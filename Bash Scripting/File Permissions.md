The Linux system follows the Unix method of ﬁle permissions, allowing individual users and groups access to ﬁles based on a set of security settings for each ﬁle and directory.

# Security
---
The core of the Linux security system is the *user account*. Each individual who accesses a Linux system should have a unique user account assigned.

User permissions are tracked using a user ID (often called a UID), which is assigned to an account when it’s created. The UID is a numerical value, unique for each user.

>**The /etc/passwd file**

The Linux system uses a special ﬁle to match the login name to a corresponding UID
value. This ﬁle contains several pieces of information about the user.

The `root` user account is the administrator for the Linux system and is always assigned
UID 0. Linux system creates lots of user accounts for various functions that aren’t actual users. These are called system accounts. A system account is a special account that services running on the system use to gain access to resources on the system.

Linux reserves UIDs below 500 for system accounts. Some services even require speciﬁc
UIDs to work properly. When you create accounts for normal users, most Linux systems
assign the ﬁrst available UID starting at 500.

The password ﬁeld in the /etc/passwd ﬁle is set to an `x`. Most Linux systems hold user passwords in a separate ﬁle (called the shadow ﬁle, located at /etc/shadow). Only special programs (such as the login program) are allowed access to this ﬁle.

> **The /etc/shadow file**

The /etc/shadow ﬁle provides more control over how the Linux system manages pass-
words. Only the root user has access to the /etc/shadow ﬁle, making it more secure than
the /etc/passwd ﬁle.
Linux system has much ﬁner control over user passwords. It can control how often a user must change his or her password and when to disable the account if the password hasn’t been changed.

## Adding a new user
---
The primary tool used to add new users to your Linux system is `useradd`. To see the system default values used on your Linux distribution, enter the `useradd` command with the -D parameter:
```bash
/usr/sbin/useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

The `useradd` command allows an administrator to create a default HOME directory conﬁguration and then uses that as a template to create the new user’s HOME directory. This allows you to place default ﬁles for the system in every new user’s HOME directory automatically.

```bash
$ ls -al /etc/skel
total 32
drwxr-xr-x   2 root root  4096 2010-04-29 08:26 .
drwxr-xr-x 135 root root 12288 2010-09-23 18:49 ..
-rw-r--r--   1 root root   220 2010-04-18 21:51 .bash_logout
-rw-r--r--   1 root root  3103 2010-04-18 21:51 .bashrc
-rw-r--r--   1 root root   179 2010-03-26 08:31 examples.desktop
-rw-r--r--   1 root root   675 2010-04-18 21:51 .profile
```

By default, the useradd command doesn’t create a HOME directory, but the `–m` command
line option tells it to create the HOME directory.

> **The useradd Command Line Parameters**

Parameter | Description
-- | --
-c comment | Adds text to the new user’s comment field
-d home_dir | Specifies a differ
-e expire_date | Specifies a date, in YYYY-MM-DD format, when the account will expire
-f inactive_days | Specifies the number of days after a password expires when the account will be disabled. A value of 0 disables the account as soon as the password expires; a value of -1 disables this feature.
-g initial_group | Specifies the group name or GID of the user’s login group
-G group . . . | Specifies one or more supplementary groups the user belongs to
-k | Copies the /etc/skel directory contents into the user’s HOME directory (must use -m as well)
-m | Creates the user’s HOME directory
-M | Doesn’t create a user’s HOME directory (used if the default setting is to create one)
-n | Creates a new group using the same name as the user’s login name
-r | Creates a system account
-p passwd | Specifies a default password for the user account
-s shell | Specifies the default login shell
-u uid | Specifies a unique UID for the account
# Removing a user
---
>`userdel` 

By default, the userdel command removes only the user information from the /etc/passwd
ﬁle. It doesn’t remove any ﬁles the account owns on the system. If you use the -r parameter, userdel removes the user’s HOME directory, along with the user’s mail directory. However, other ﬁles owned by the deleted user account may still be on the system.

```bash
/usr/sbin/userdel -r <user>
```

# Modifying a user
---
> **User Account Modification Utilities**

Command | Description
-- | --
usermod | Edits user account fields, as well as specifying primary and secondary group membership
passwd | Changes the password for an existing user
chpasswd | Reads a file of login name and password pairs, and updates the passwords
chage | Changes the password’s expiration date
chfn | Changes the user account’s comment information
chsh | Changes the user account’s default shell
>The **usermod** provides options for changing most of the ﬁelds in the /etc/passwd ﬁle.
- `-l` changes the login name of the user account
- `-L` locks the account so the user can't log in
- `-p` changes the password for the account
- `-U` unlocks the account so the user can log in.

>The **passswd** and **chpasswd**

```bash
passwd test
```
If we just use the passwd command by itself, it changes our own password. Any user in
the system can change his or her own password, but only the **root** user can change someone else’s password.

If we ever need to do a mass password change for lots of users on the system, the chpasswd command can be a lifesaver. The chpasswd command reads a list of login name
and password pairs (separated by a colon) from the standard input, automatically encrypts
the password, and sets it for the user account.
```bash
chpasswd < users.txt
```

> The **chsh** command allows us to quickly change the default login shell for a user. We must use the full path name for the shell.

```bash
chsh -s /bin/csh
```

> The chfn command provides a standard method for storing information in the comments ﬁeld in the /etc/passwd ﬁle. If you use the chfn command with no parameters, it queries you for the appropriate values to enter in to the comment ﬁeld.

- `finger` command --> ﬁnds information about people on our Linux system.

> The **chage** command helps you manage the password ageing process for user accounts.

# Linux Groups
---
Group permissions allow multiple users to share a common set of permissions for an object
on the system, such as a ﬁle, directory, or device. Each group has a unique GID, which, like UIDs, is a unique numerical value on the system. Along with the GID, each group has a unique group name. You can use some group utilities to create and manage your own groups on the Linux system.

> The **/etc/group** file

The /etc/group ﬁle contains information about each group used on the system. Groups used for system accounts are assigned GIDs below 500, and user groups are assigned GIDs starting at 500.

This file contains four fields:
- The group name
- The group password
- The GID
- The list of user accounts that belong to the group

We should never add users to groups by editing the /etc/group ﬁle. Instead, use the  `usermod` command  to add a user account to a group.

> **Creating new groups**

```bash
/usr/sbin/groupadd <groupname>
```

The groupadd command doesn’t provide an option for adding user accounts to the group. Instead, to add new users, use the usermod command
```bash
/usr/sbin/usermod -G <groupname> <user>
```

The `-G` parameter in `usermod` appends the new group to the list of groups for the user account.

>**Modifying groups**

The groupmod command allows you to change the GID (using the -g parameter) or the group name (using the -n parameter) of an existing group.
```bash
/usr/sbin/groupmod -n <oldname> <newname>
```

# Debunking File Permissions
---
> Familiarising file permission symbols

1. The ﬁrst ﬁeld in the output listing is a code that describes the permissions for the ﬁles and directories.
	- `-`  for files
	- `d` for directories
	- `l` for links
	- `c` for character devices
	- `b` for block devices
	- `n` for network devices
2. File Permissions
	- `r` for read permission
	- `w` for write permission
	- `x` for execute permission
3. The file permissions occurs in groups of three for `owner`, `group`, `everyone else`.

> The `umask` command sets the default permissions for any file or directory that we create.

> **Linux File Permission Codes**

Permissions | Binary | Octal | Description
-- | -- | -- | --
--- | 000 | 0 | No permissions
--x | 001 | 1 | Execute-only permission
-w- | 010 | 2 | Write-only permission
-wx | 011 | 3 | Write and execute permissions
r-- | 100 | 4 | Read-only permission
r-x | 101 | 5 | Read and execute permissions
rw- | 110 | 6 | Read and write permissions
rwx | 111 | 7 | Read, write, and execute permissions

## Changing Permissions
---
> The **chmod** command allows us to change the security settings for ﬁles and directories.

```bash
chmod options mode file
```

The following is the format for specifying a permission in symbolic mode:
```bash
[ugoa…][[+-=][rwxXstugo…]
```

The first group of characters defines to whom the new permissions apply:
- `u` --> user
- `g` --> group
- `o` --> others
- `a` --> all of the above
We can use wildcard characters for the ﬁlename speciﬁed, changing the permissions on
multiple ﬁles with just one command.

> The **chown** command used to change the owner of a ﬁle.

```bash
chown options owner[.group] file
```

Only the root user can change the owner of a file. Any user can change the default group of a file, but the user must be a member of the groups the file is changed from and to.
