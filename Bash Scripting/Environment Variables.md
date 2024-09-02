Many programs and scripts use environment variables to obtain system information and store temporary data and conﬁguration information.

# Exploring Environment Variables
---
The bash shell uses a feature called environment variables to store information about the shell session and the working environment.

Environment variable types :
- `Global variables`
- `Local variables`

> **Global Environment Variables**

Global environment variables are visible from the shell session and from any spawned child
sub-shells. Local variables are available only in the shell that creates them. The system environment variables almost always use all `capital letters` to differentiate them from normal user environment variables.

To view global environment variables, use the `env` or `printenv` command:
```bash
printenv
```

To display an individual environment variable’s value, we can use the printenv command, but not the env command:
```bash
printenv HOME
```

To print the variable value to the terminal,
```bash
echo $HOME
```

The dollar sign before a variable name allows the variable to be passed as a command parameter
```bash
ls $HOME # is same as
ls /jarvis/home/
```

> **Local Environment Variables**

They can be seen only in the local process in which they are deﬁned. There isn't a command that displays only these variables. The `set` command displays all variables
deﬁned for a speciﬁc process, including both local and global environment variables and
user-deﬁned variables. It also sorts the display **alphabetically**.

# Setting User-Defined Variables
---
> **Local** user-defined variables

We can assign either a numeric or a string value to an environment variable by assigning the variable to a value using the equal sign.
```bash
my_variable=Hello
echo $my_variable

Hello
```

If we need to assign a string value that contains spaces, we need to use a single or double
quotation mark. It’s extremely important that we not use spaces between the variable name, the equal sign, and the value. If we put any spaces in the assignment, the bash shell interprets the value as a separate command.

After you set a local variable, it’s available for use anywhere within our shell process.
However, if we spawn another shell, it’s not available in the child shell. Also the local variable set within the child shell doesn’t exist after a return to the parent shell.

>Setting **Global** Environment variables

Global environment variables are visible from any child processes created by the parent process that sets the variable. The method used to create a global environment variable is to ﬁrst create a local variable and then export it to the global environment.
```bash
my_variable=Hello
export my_variable
```

Changing a global environment variable within a child shell does not affect the variable’s
value in the parent shell. A child shell cannot even use the export command to change the parent shell’s global environment variable’s value.

# Removing Environment Variables
---
To remove an existing environment variable
```bash
unset <variableName>
```

- `When to use the $ `

>If you are doing anything with the variable, use the dollar sign. If you are doing anything to the variable, don’t use the dollar sign.

If you’re in a child process and unset a global environment variable, it applies only to the child process. The global environment variable is still available in the parent process.

# Setting the PATH Environment Variable
---
When we enter an external command in the CLI, the shell must search the system to find the program. The `PATH` environment variable defines the directories it searches looking for commands and programs.

The problem is that often applications place their executable programs in directories that
aren’t in the PATH environment variable. We can add new search directories to the existing PATH environment variable without having to rebuild it from scratch.
```bash
PATH=$PATH:/path
export PATH
```

By adding the directory to the PATH environment variable, we can now execute your
program from anywhere in the virtual directory structure.

A common trick for programmers is to include the single dot symbol in their PATH environment variable.
```bash
PATH=$PATH:.
```

# Locating System Environment Variables
---
When we start a bash shell by logging in to the Linux system, by default bash checks
several ﬁles for commands. These ﬁles are called startup files or environment files.

You can start a bash shell in three ways:
- As a default login shell at login time
- As an interactive shell that is started by spawning a subshell
- As a non-interactive shell to run a script

When we log in to the Linux system, the bash shell starts as a login shell. The `/etc/profile` ﬁle is the main default startup ﬁle for the bash shell on the system. All users on the system execute this startup ﬁle when they log in.

>**Understanding the interactive shell process**

If you start a bash shell without logging into a system, you start what’s called an interactive shell. The interactive shell doesn’t act like the login shell, but it still provides a CLI prompt for you to enter commands.
If bash is started as an interactive shell, it doesn’t process the /etc/profile ﬁle. Instead,
it only checks for the .bashrc ﬁle in the user’s HOME directory.

> **Understanding the non-interactive shell process**

This is the shell where the system can start to execute a shell script. When the shell starts a non-interactive subshell process, it checks BASH_ENV environment variable for the startup ﬁle name to execute. If one is present, the shell executes the ﬁle’s commands, which typically include variables set for the shell scripts.

# Variable Arrays
---
A really cool feature of environment variables is that they can be used as arrays. To set multiple values for an environment variable, just list them in parentheses, with values separated by spaces
```bash
mytest=(one two three four five)
```

```bash
echo $mytest  # one
echo ${mytest[1]} # two
echo ${mytest[*]} # one two three four five
unset mytest[2]
echo ${mytest[2]} # 
unset mytest
```
