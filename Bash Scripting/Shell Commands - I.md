# Shell
---
The GNU bash shell is a program that provides interactive access to the Linux system. It runs as a regular program and is normally started whenever a user logs in to a terminal.
The **/etc/passwd**  ﬁle contains a list of all the system user accounts, along with some basic conﬁguration information about each user.

The default prompt symbol for the bash shell is the dollar sign ($).

Most Linux distributions include an online manual for looking up information on shell
commands, as well as lots of other GNU utilities included in the distribution. The **man** command provides access to the manual pages stored on the Linux system.

# Navigating the File System
---
When you log into the system and reach the shell command prompt, you are usually placed
in your home directory.
## Linux File System
---
Linux stores ﬁles within a single directory structure, called a virtual directory. The virtual directory contains ﬁle paths from all the storage devices installed on the computer, merged into a single directory structure. 

>Linux uses a forward slash (/) instead of a backward slash (\) to denote directories in file paths. The backslash character in Linux denotes an escape character and causes all sorts of problems when you use it in a file path.

The tricky part about the Linux virtual directory is how it incorporates each storage device.
The ﬁrst hard drive installed in a Linux system is called the **root drive**. The root drive contains the virtual directory core.

On the root drive, Linux can use special directories as *mount points*. Mount points are
directories in the virtual directory where you can assign additional storage devices. Linux
causes ﬁles and directories to appear within these mount point directories, even though
they are physically stored on a different drive.

**Common Linux Directory Names**

| Directory | Usage                                                                              |
| --------- | ---------------------------------------------------------------------------------- |
| /         | root of the virtual directory, where normally, no files are placed                 |
| /bin      | binary directory, where many GNU user-level utilities are stored                   |
| /boot     | boot directory, where boot files are stored                                        |
| /dev      | device directory, where Linux creates device nodes                                 |
| /etc      | system configuration files directory                                               |
| /home     | home directory, where Linux creates user directories                               |
| /lib      | library directory, where system and application library files are stored           |
| /media    | media directory, a common place for mount points used for removable media          |
| /mnt      | mount directory, another common place for mount points used for<br>removable media |

When you log in to your system and reach a shell CLI prompt, your session starts in your
home directory. Your home directory is a unique directory assigned to your user account.
When a user account is created, the system normally assigns a unique directory for the
account.

## Traversing Directories
---
You use the change directory command (cd) to move your shell session to another directory
in the Linux ﬁle system.

```bash
cd destination
```

The cd command may take a single parameter, destination, which speciﬁes the directory
name you want to go to. If you don’t specify a destination on the cd command, it takes you
to your home directory.

```bash
pwd
```
 The pwd command displays the shell session’s current directory location, which is called the **present working directory**.
 
### Using absolute directory references
---
The absolute directory reference deﬁnes exactly where the directory is in the virtual directory structure, starting at the root. An absolute directory reference always begins with a forward slash (/), indicating the virtual directory system’s root.

### Using relative directory references
---
Relative directory references allow you to specify a destination directory reference relative to your current location. A relative directory reference doesn’t start with a forward slash (/).

The two special characters used for relative directory references are:
- The single dot (.) to represent the current directory
- The double dot (..) to represent the parent directory

## Listing Files and Directories
---
```bash
ls
```
At its most basic form displays the ﬁles and directories located in your current directory. In Linux, hidden ﬁles are ﬁles with ﬁlenames starting with a period (.). These ﬁles don’t appear in the default ls listing.

To display hidden ﬁles along with normal ﬁles and directories:
```bash
ls -a
```

```bash
ls -F
```
The -F parameter ﬂags the directories with a forward slash (/), to help identify them in
the listing. Similarly, it ﬂags executable ﬁles with an asterisk (*), to help you more easily ﬁnd ﬁles that can be run on the system.

```bash
ls -R
```
The -R parameter is another option the ls command can use. Called the recursive option,
it shows ﬁles that are contained within sub-directories in the current directory.

**Important to note here that**
```bash
ls -F -R # is same as
ls -FR
# We can combine flags.
```

In the basic listings, the ls command doesn’t produce much information about each ﬁle.
```bash
ls -l
```
The long listing format lists each ﬁle and sub-
directory on a single line. In addition to
the ﬁlename, the listing shows additional useful information.
- The ﬁle type — such as directory (d), ﬁle (-), linked ﬁle (l), character device (c), or block device (b)
- The ﬁle permissions
- The number of ﬁle hard links
- The ﬁle owner username
- The ﬁle primary group name
- The ﬁle byte size
- The last time the ﬁle was modiﬁed
- The ﬁlename or directory name

The ls command also provides a way for you to deﬁne a ﬁlter on the command line. It uses the ﬁlter to determine which ﬁles or directories it should display in the output. 
```bash
ls -l <filename or dirname>
```
When you specify the name of a speciﬁc ﬁle as the ﬁlter, the ls command only shows that ﬁle’s information.

The ls command also recognises standard wildcard characters and uses them to match
patterns within the ﬁlter
```bash
ls -l my_scr?pt  #question mark can be used to replace exactly one character anywhere in the ﬁlter string
ls -l my*  #asterisk can be used to match zero or more characters
```

Using the asterisk and question mark in the ﬁlter is called ﬁle **globbing**. File globbing is the
processing of pattern matching using wildcards.
```bash
ls -l my_sc[ai]pt #search for a or i
ls -l my_sc[a-i]pt #searches between a to i
```

The *inode* number of a ﬁle or directory is a unique identiﬁcation number that the kernel assigns to each object in the ﬁle system. To view a ﬁle or directory’s inode number
```bash
ls -i <filename>
```

# Handling Files
---
The shell provides many ﬁle manipulation commands on the Linux ﬁle system.
## Creating Files
---
To create an empty file:

```bash
touch <filename>
```
The touch command creates the new ﬁle you specify and assigns your username as the ﬁle
owner. This command can also be used to modify the time stamp of the file.

## Copying Files
---
>To **`copy`** a file:

```bash
cp <source> <destination>
cp -i <source> <destination> # overwrites if the file alrady exists in destination.
```
If the destination ﬁle already exists, the cp command may not prompt you to this fact. It is best to add the -i option to force the shell to ask whether you want to overwrite a ﬁle.

The -R parameter is a powerful cp command option. It allows you to recursively copy the
contents of an entire directory.
```bash
cp -R <source> <destination>
```

**Wildcard meta characters** can also be used in cp commands.

## Linking Files
---
If we need to maintain two (or more) copies of the same ﬁle on the system, instead of having separate physical copies, we can use one physical copy and multiple virtual copies, called **links**. A link is a placeholder in a directory that points to the real location of the ﬁle.

- A *symbolic link* is simply a physical ﬁle that points to another ﬁle somewhere in the virtual directory structure. The two symbolically linked together ﬁles do not share the same contents.
	- To create a symbolic link to a file, the original must preexist.
	-  The symbolic link only points to the original file not to the contents of the file. The size of both the files differ.
```bash
ln -s <filename> <symbolicFileName> #ln with -s flag creates a symbolic link.
```

- A *hard link* creates a separate virtual ﬁle that contains information about the original ﬁle and where to locate it. However, they are physically the same ﬁle.
	- To create a hard link, the original file must preexist.
	- The files, which are hard linked share the same inode number. Their size is same as well.
```bash
ln <filename> <hardlinkFileName>
```

> If we delete the original file and all the files that are hard linked to this file works fine. However when the files are soft linked the deletion of the original file breaks the links and the linked files will be broken.

## Renaming and Deleting Files
---
In the Linux terminology, renaming files is basically *moving files*.

```bash
mv <filename> <newFilename>
# -i overwrites if the file already exists.
```
mv command only affects the file name. so the inode number and timestamp remains intact. It can also be used to change file location.

```bash
mv <filename> <destination>
```
Neither the timestamp value nor the inode number changes. Only the location and name were altered.

The command to remove files in the bash shell is **rm**. The shell has no recycle bin. After we remove a file, it's gone forever. The use of -i is good practice and prevents us from deleting important files accidentally.

```bash
rm -i <filename> # -i asks for confirmation.
```
We can also use wildcard **meta characters** to remove groups of ﬁles.

# Managing Directories
---
Linux has a few commands that work for both ﬁles and directories (such as the cp command), and some that work only for directories.

## Creating directories
---
>To create a directory:

```bash
mkdir New_dir
ls -ld New_dir
drwxrwxr-x 2 christine christine 4096 May 22 09:48 New_dir
```
Notice in the new directory’s long listing that the directory’s record begins with a d. This indicates that New_dir is not a ﬁle, but a directory.

>To create several directories and sub-directories at the same time, use -p flag:

```bash
mkdir -p New_dir/sub_dir/sub_sub_dir/
```

## Removing Directories
---
There are lots of opportunities for bad things to happen when we start deleting directories. The shell tries to protect us from accidental catastrophes as much as possible.

>To remove a directory

```bash
rmdir <dirname>
```
By default, the above command only works for empty directories. The **rmdir** has no -i option to ask if you want to remove the directory.

We can also use the rm command on entire non-empty directories. But we need to use the -r flag which allows the command to descend into the directory, remove the files, and then remove the directory itself.

```bash
rm -ri <dirname> # i--> for confirmation
```
For a directory with lots of ﬁles and sub-directories, this can become tedious. The ultimate solution for throwing caution to the wind and removing an entire directory, contents and all, is the rm command with both the -r and -f parameters.

```bash
rm -rf <dirname>
```

**`Cool Tip`**

```bash
tree <dirname> # Creates a cool tree showing correlation between directories.
```

# Viewing File Contents
---
The file command is a handy little utility to have around. It can peek inside of a ﬁle and determine just what kind of ﬁle it is

```bash
file <filename>
file sl <filename>  #tells you to which ﬁle it is symbolically linked
```

## Viewing the whole file
---
>**cat** command:

```bash
cat <filename>
# -n --> numbers all the lines.
# -b --> numbers the lines that have text in them.
# -T --> replaces any tabs in the text with ^I character.

```
The main drawback of the cat command is that you can’t control what’s happening after you start it.

>**more** command:

```bash
more <filename>
```
The more command displays a text ﬁle, but stops after it displays each page of data. We  can use more to navigate through a text ﬁle by pressing the space bar or you can go forward line by line using the Enter key. When you are ﬁnished navigating through the ﬁle using more, press the q key to quit.

>**less** command:

```bash
less <filename>
```
The less command name is actually a play on words and is an advanced version of the more command. It can also display a ﬁle’s contents before it ﬁnishes reading the entire ﬁle. The cat and more commands cannot do this.

## Viewing parts of a file
---
>**head** command:

```bash
head <filename>
head -n <number> <filename>
```
The head command displays a ﬁle’s ﬁrst group of lines (the ﬁle’s “head”). By default, it displays the ﬁrst 10 lines of text. We can change the number of lines shown using head by including the -n parameter.

>**tail** command:

```bash
tail <filename>

```
The tail command displays the last lines in a ﬁle (the ﬁle’s “tail”). By default, it shows the last 10 lines in the ﬁle. Similar to the head command the tail command also supports the -n parameter.