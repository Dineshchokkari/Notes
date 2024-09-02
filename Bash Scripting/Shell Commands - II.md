# Monitoring Programs
---
When a program runs on the system, it’s referred to as a *process*. The **ps** command can produce lots of information about all the programs running on our system. By default, the ps command shows only the processes that belong to the current user and that are running on the current terminal.
The basic output shows the process ID (PID) of the programs, the terminal (TTY) that they are running from, and the CPU time the process has used.

**Process Terminology**
- **UID** --> The user responsible for launching the process.
- **PID** --> The process ID of the process.
- **PPID** --> The PID of the parent process.
- **C** --> Processor utilisation over the lifetime of the process.
- **STIME** --> The system time when the process started.
- **TTY** -->  The terminal device from which the process was launched.
- **TIME** --> The cumulative CPU time required to run the process.
- **CMD** --> The name of the program that was started.
- **VSZ** --> The size in kilobytes of the process in memory.
- **RSS** --> The physical memory that a process has used that isn’t swapped out.
- **STAT** --> A two-character state code representing the current process state.

The GNU ps command that’s used in Linux systems supports three different types of command line parameters:
- **Unix-style** parameters, which are *preceded by a dash*
- **BSD-style** parameters, which are *not preceded by a dash*
- **GNU long** parameters, which are *preceded by a double dash*

**The ps Command Unix Parameters**

Parameter | Description
-- | --
-A | Shows all processes
-N | Shows the opposite of the specified parameters
-a | Shows all processes except session headers and processes without a terminal
-d | Shows all processes except session headers
-e | Shows all processes
-C cmslist | Shows processes contained in the list cmdlist
-G grplist | Shows processes with a group ID listed in grplist
-U userlist | Shows processes owned by a userid listed in userlist
-g grplist | Shows processes by session or by groupid contained in grplist
-p pidlist | Shows processes with PIDs in the list pidlist
-s sesslist | Shows processes with session ID in the list sesslist
-t ttylist | Shows processes with terminal ID in the list ttylist
-u userlist | Shows processes by effective userid in the list userlist
-F | Uses extra full output
-O format | Displays specific columns in the list format, along with the default columns
-M | Displays security information about the process
-c | Shows additional scheduler information about the process
-f | Displays a full format listing
-j | Shows job information
-l | Displays a long listing
-o format | Displays only specific columns listed in format
-y | Prevents display of process flags
-Z | Displays the security context information
-H | Displays processes in a hierarchical format (showing parent processes)
-n namelist | Defines the values to display in the WCHAN column
-w | Uses wide output format, for unlimited width displays
-L | Shows process threads
-V | Displays the version of p

**The ps Command BSD Parameters**

Parameter | Description
-- | --
T | Shows all processes associated with this terminal
a | Shows all processes associated with any terminal
g | Shows all processes including session headers
r | Shows only running processes
x | Shows all processes, even those without a terminal device assigned
U userlist | Shows processes owned by a userid listed in userlist
p pidlist | Shows processes with a PID listed in pidlist
t ttylist | Shows processes associated with a terminal listed in ttylist
O format | Lists specific columns in format to display along with the standard columns
X | Displays data in the register format
Z | Includes security information in the output
j | Shows job information
l | Uses the long format
o format | Displays only columns specified in format
s | Uses the signal format
u | Uses the user-oriented format
v | Uses the virtual memory format
N namelist | Defines the values to use in the WCHAN column
O order | Defines the order in which to display the information columns
S | Sums numerical information, such as CPU and memory usage, for child processes into the parent process
c | Displays the true command name (the name of the program used to start the process)
e | Displays any environment variables used by the command
f | Displays processes in a hierarchical format, showing which processes started which processes
h | Prevents display of the header information
k sort | Defines the column(s) to use for sorting the output
n | Uses numeric values for user and group IDs, along with WCHAN information
w | Produces wide output for wider terminals
H | Displays threads as if they were processes
m | Displays threads after their processes
L | Lists all format specifiers
V | Displays the version of ps
When we use the BSD-style parameters, the ps command automatically changes the output
to simulate the BSD format.

## Real-time process monitoring
---
The ps command can display information only for a speciﬁc point in time. If you’re trying to ﬁnd trends about processes that are frequently swapped in and out of memory, it’s hard to do that with the ps command. The **top** command displays process information similarly to the ps command, but it does it in real-time mode.

**Top Command Terminology**
- **PID** --> The process ID of the process
- **USER** --> The user name of the owner of the process
- **PR** --> The priority of the process
- **NI** --> The nice value of the process
- **VIRT** --> The total amount of virtual memory used by the process
- **RES** --> The amount of physical memory the process is using
- **SHR** --> The amount of memory the process is sharing with other processes
- **S** --> The process status (D = interruptible sleep, R = running, S = sleeping, T = traced or stopped, or Z = zombie)
- **%CPU** --> The share of CPU time that the process is using
- **%MEM** --> The share of available physical memory the process is using
- **TIME+** --> The total CPU time the process has used since starting
- **COMMAND** --> The command line name of the process (program started)

## Stopping Processes
---
Sometimes, a process gets hung up and needs a gentle nudge to either get going again or stop. Other times, a process runs away with the CPU and refuses to give it up. In both cases, we need a command that allows you to control a process.

In Linux, processes communicate with each other using *signals*. A process signal is a predeﬁned message that processes recognise and may choose to ignore or act on.

**Linux Process Signals**

| Signal | Name | Description                                         |
| ------ | ---- | --------------------------------------------------- |
| 1      | HUP  | Hangs up                                            |
| 2      | INT  | Interrupts                                          |
| 3      | QUIT | Stops running                                       |
| 9      | KILL | Unconditionally terminates                          |
| 11     | SEGV | Produces segment violation                          |
| 15     | TERM | Terminates if possible                              |
| 17     | STOP | Stops unconditionally, but doesn’t terminate        |
| 18     | TSTP | Stops or pauses, but continues to run in background |
| 19     | CONT | Resumes execution after STOP or TSTP                |
>The **kill** command allows you to send signals to processes based on their process ID (PID). By default, the kill command sends a TERM signal to all the PIDs listed on the command line.

```bash
kill <PID>
```
To send a process signal, you must either be the owner of the process or be logged in as the root user. The TERM signal tells the process to kindly stop running. Unfortunately, if you have a runaway process, most likely it ignores the request. When you need to get forceful, the -s parameter allows you to specify other signals.

> The **killall** command is a powerful way to stop processes by using their names rather than the PID numbers. The killall command allows you to use wildcard characters as well.

# [[Introduction To Linux| Monitoring Disk Space]]
---
The Linux ﬁle system combines all media disks into a single virtual directory. Before you can use a new media disk on your system, you must place it in the virtual directory. This task is called **mounting**. 

## Mounting media
---
> The **mount** command

```bash
mount
```
It provides four pieces of information:
- The device filename of the media.
- The mount point in the virtual directory where the media is mounted.
- The file system type.
- The access status of the mounted media.

> To manually mount a media device, you must be logged in as the root user or use the sudo command to run the command as the root user. After a media device is mounted in the virtual directory, the root user has full access to the device, but access by other users is restricted.

```bash
mount -t type device directory
# type --> filesystem type such as ntfs, vfat, etc.
# device --> location of the device file for the media device
# directory --> location of the mount point in the virtual directory.
```


Linux recognises lots of different ﬁle system types. If you share removable media devices with your Windows PCs, you are most likely to run into these types:
- vfat: Windows long ﬁle system
- ntfs: Windows advanced ﬁle system used in Windows NT, XP, and Vista
- iso9660: The standard CD-ROM ﬁle system

Most USB memory sticks and ﬂoppies are formatted using the vfat ﬁle system. If we need
to mount a data CD, we must use the iso9660 ﬁle system type. 

> The **umount** command

To remove a removable media device, you should never just remove it from the system.
Instead, you should always unmount it ﬁrst.

```bash
umount [directory | device]
# we can specify directory or device location of the media device
```
If any program has a ﬁle open on a device, the system won’t let you unmount it.

> The **df** command allows you to easily see what’s happening on all the mounted disks.

It displays the following
- The device location of the device.
- How many 1024-byte blocks of data it can hold
- How many 1024-byte blocks are used
- How many 1024-byte blocks are available
- The amount of used space as a percentage
- The mount point where the device is mounted

```bash
df -h   # makes the output human readable
```

The values from the df command reflect what the Linux system thinks are the current values at that point in time. It’s possible that you have a process running that has created or deleted a file but has not released the file yet. This value is not included in the free space calculation.

> The **du** command shows the disk usage for a speciﬁc directory (by default, the current directory).

By default, the du command displays all the ﬁles, directories, and sub-directories under the current directory, and it shows how many disk blocks each ﬁle or directory takes. The number at the left of each line is the number of disk blocks that each ﬁle or directory takes.

```bash
du -c -h -s
# c--> produces a grand totoal of all the files listed.
# h--> Prints sizes in human-readable form, using K for kilobyte, M for megabyte, and G for gigabyte.
# s--> Summarises each argument.
```

# Working with Data Files
---
> The **sort** command

By default, the sort command sorts the data lines in a text file using standard sorting rules for the language.

```bash
cat abc.txt
one
two
three
four
five
sort abc.txt
five
four
one
six
three
two
```
 But things aren’t always as easy as they appear.

```bash
cat abc.txt 
1
2
100
45
3
sort abc.txt 
1
100
2
3
45
```
By default, the sort command interprets numbers as characters and performs a standard
character sort, producing output that might not be what you want. Use the -n parameter, to treat them as numbers instead of characters.

```bash
sort -n <filename> #treats the characters as numbers for numerological sort.
sort -M <filename> # sorts on the basis of timestamp.
```

**Parameters for the sort command**

Single Dash | Double Dash | Description
-- | -- | --
-f | --ignore-case | By default, sort orders capitalised letters first; ignores case
-k | --key = POS | Sorts based on position POS
-M | --month-sort | Sorts by month order using three-character month names
-m | --merge | Merges two already sorted data files
-n | --numeric-sort | Sorts by string numerical value
-o | --output = file | Writes results to file specified
-r | --reverse | Reverses the sort order (descending instead of ascending)
-t | --field-separator = SEP | Specifies the character used to distinguish key positions

## Searching for Data
---
> The **grep** command

```bash
grep [options] pattern [file]
# -v --> outputs the lines that don't match the pattern.
# -n --> finds the line numbers where the matching patterns are found.
# -c --> counts the output of -n
# -e --> enable to provide more than one matching pattern. use for each individual pattern.
```
It searches either the input or the ﬁle you specify for lines that contain characters that match the speciﬁed pattern. 
grep also supports **regular expressions.**

## Compressing Data
---
Linux contains several ﬁle compression utilities. Although this may sound great, it often
leads to confusion and chaos when trying to download ﬁles.

> **Linux File Compression Utilities**

Utility | File Extension | Description
-- | -- | --
bzip2 | .bz2 | Uses the Burrows-Wheeler block sorting text compression algorithm and Huffman coding
compress | .Z | Original Unix file compression utility; starting to fade away into obscurity
gzip | .gz | The GNU Project’s compression utility; uses Lempel-Ziv coding
zip | .zip | The Unix version of the PKZIP program for Windows
The gzip utility is the most popular compression tool used in Linux. The gzip package is a creation of the GNU Project, in their attempt to create a free version of the original Unix compress utility.

> The **gzip** command

It compresses the ﬁle you specify on the command line. You can also specify more than one ﬁlename or even use wildcard characters to compress multiple ﬁles at once. 

> The **gunzip** command unzips the compressed files.

Although the zip command works great for compressing and archiving data into a single ﬁle, it’s not the standard utility used in the Unix and Linux worlds.
## Archiving Data
---
> The **tar** command

```bash
tar function [options] obj1 obj2 ...
```

> **The tar Command Functions**

| Function | Long Name     | Description                                                                                                         |
| -------- | ------------- | ------------------------------------------------------------------------------------------------------------------- |
| -A       | --concatenate | Appends an existing tar archive file to another existing tar archive file                                           |
| -c       | --create      | Creates a new tar archive file                                                                                      |
| -d       | --diff        | Checks the differences between a tar archive file and the filesystem                                                |
|          | --delete      | Deletes from an existing tar archive file                                                                           |
| -r       | --append      | Appends files to the end of an existing tar archive file                                                            |
| -t       | --list        | Lists the contents of an existing tar archive file                                                                  |
| -u       | --update      | Appends files to an existing tar archive file that are newer than a file with the same name in the existing archive |
| -x       | --extract     | Extracts files from an existing archive file                                                                        |

>**The tar Command Options**

Option | Description
-- | --
-C dir | Changes to the specified directory
-f file | Outputs results to file (or device) file
-j | Redirects output to the bzip2 command for compression
-p | Preserves all file permissions
-v | Lists files as they are processed
-z | Redirects the output to the gzip command for compression
Filenames that end in .tgz. These are gzipped tar files, which can be extracted using the command
```bash
tar -zxvf filename.tgz
```
