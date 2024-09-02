Four main parts make up a **Linux System.**
1. The Linux Kernel
2. The GNU Utilities
3. A graphical desktop environment
4. Application software

![[LinuxSystem.png]]


# 1. The Linux Kernel
---
The core of the Linux system is the *Kernel*. The kernel controls all the hardware and software on the computer system, allocating hardware when necessary and executing software when required.

**Linus Torvalds** developed the Linux Kernel and released it to the Internet community and solicited suggestions for improving it.

The main functions of kernel are:
1. System memory management
2. Software program management
3. Hardware management
4. File system management

## 1.1. System Memory Management
---
Not only does the kernel manage the physical memory available on the server, but it can also create and manage virtual memory, or memory that does not actually exist. It does this by using space on the hard disk, called the swap space. The kernel swaps the contents of virtual memory locations back and forth from the swap space to the actual
physical memory.

The memory locations are grouped into blocks called pages. The kernel locates each page
of memory either in the physical memory or the swap space. The kernel then maintains a
table of the memory pages that indicates which pages are in physical memory and which
pages are swapped out to disk.

## 1.2. Software Program Management
---
The Linux operating system calls a running program a *process*. A process can run in the
foreground, displaying output on a display, or it can run in the background, behind the
scenes.

The kernel creates the ﬁrst process, called the init process, to start all other processes on the system. When the kernel starts, it loads the init process into virtual memory. As the kernel starts each additional process, it gives it a unique area in virtual memory to store the data and code that the process uses.

The Linux operating system uses an init system that utilises run levels. A run level can be
used to direct the init process to run only certain types of processes.
1. At run level 1, only the basic system processes are started, along with one console terminal process. This is called *single-user* mode.
2. The standard init run level is 3. At this run level, most application software, such as network support software, is started.
3. At run level 5, the system starts the graphical X Window software and allows you to log in using a graphical desktop window.
## 1.3. Hardware Management
---
Any device that the Linux system must communicate with needs driver code inserted inside the kernel code. The driver code allows the kernel to pass data back and forth to the device, acting as a middle man between applications and the hardware.

Methods used for inserting device driver code in the Linux Kernel:
1. Drivers compiled in the kernel
2. Driver modules added to the kernel

Previously, the only way to insert device driver code was to recompile the kernel. Each time
you added a new device to the system, you had to recompile the kernel code. Programmers developed the concept of kernel modules to allow you to insert driver code into a running kernel without having to recompile the kernel.

The Linux system identiﬁes hardware devices as special ﬁles, called *device files*. There are
three classiﬁcations of device ﬁles
1. **Character device ﬁles** are for devices that can only handle data one character at a time.
2. **Block ﬁles** are for devices that can handle data in large blocks at a time, such as disk drives.
3. The **network ﬁle** types are used for devices that use packets to send and receive data.

Linux creates special ﬁles, called *nodes*, for each device on the system. All communication
with the device is performed through the device node.

## 1.4. File System Management
---
Linux kernel can support different types of ﬁle systems to read and write data to and from hard drives. Besides having over a dozen ﬁle systems of its own, Linux can read and write to and from ﬁle systems used by other operating systems, such as Microsoft Windows.

![[File Systems.png]]

Any hard drive that a Linux server accesses must be formatted using one of the ﬁle system
types listed in the above Table.
The Linux kernel interfaces with each ﬁle system using the Virtual File System (VFS). This
provides a standard interface for the kernel to communicate with any type of ﬁle system.

# 2. The GNU Utilities
---
Besides having a kernel to control hardware devices, a computer operating system needs
utilities to perform standard functions, such as controlling ﬁles and programs. The GNU organisation (GNU stands for GNU’s Not Unix) developed a complete set of Unix utilities, but had no kernel system to run them on.

These utilities were developed under a software philosophy called **open source software** (OSS). The concept of OSS allows programmers to develop software and then release it to the world with no licensing fees attached. Anyone can use the software, modify it, or incorporate it into his or her own system without having to pay a license fee.

The core bundle of utilities supplied for Linux systems is called the core-utils package.
The GNU core-utils package consists of three parts:
1. Utilities for handling ﬁles
2. Utilities for manipulating text
3. Utilities for managing processes

## [[Shell Commands - I|The Shell]]
---
The GNU/Linux shell is a special interactive utility. It provides a way for users to start pro-
grams, manage ﬁles on the ﬁle system, and manage processes running on the Linux system.
The core of the shell is the command prompt. The command prompt is the interactive part
of the shell. It allows you to enter text commands, and then it interprets the commands
and executes them in the kernel.

The default shell used in all Linux distributions is the bash shell. The bash shell was developed by the GNU project as a replacement for the standard Unix shell, called the Bourne shell (after its creator). The bash shell name is a play on this wording, referred to as the “Bourne again shell.”

**Linux Shells**

| Shell | Description                                                                                                                                                  |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ash   | A simple, lightweight shell that runs in low-memory environments but has full compatibility with the bash shell                                              |
| korn  | A programming shell compatible with the Bourne shell but supporting advanced programming features like associative arrays and floating-point arithmetic      |
| tcsh  | A shell that incorporates elements from the C programming language into shell scripts                                                                        |
| zsh   | An advanced shell that incorporates features from bash, tcsh, and korn, providing<br>advanced programming features, shared history files, and themed prompts |

# Linux Distributions
---
A complete Linux system package is called a *distribution*. Many different Linux distributions are available to meet just about any computing requirement you could have. Most distributions are customised for a speciﬁc user group, such as business users, multimedia enthusiasts, software developers, or average home users.