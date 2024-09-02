> Using Multiple Commands

The shell allows us to chain commands together into a single step. If we want to run two commands together, we can enter them on the same prompt line, separated with a semicolon.
```bash
date; whoami
```

# Creating a Script File
---
When creating a shell script ﬁle, you must specify the shell you are using in the ﬁrst line of
the ﬁle --> `#! /bin/bash`

In a normal shell script line, the pound sign (#) is used as a comment line. A comment line
in a shell script isn’t processed by the shell. However, the ﬁrst line of a shell script ﬁle is
a special case, and the pound sign followed by the exclamation point tells the shell what
shell to run the script under.

The shell processes commands in the order in which they appear in the ﬁle. This file doesn't have `execute` permissions. Use the following to change that --> `chmod a+x <filename>`

# Displaying Messages
---
> The echo command can display a simple text string
```bash
echo This is a test
This is a test
```

By default we don't need to use quotes to delineate the string we're displaying. However, sometimes this can get tricky if we are using quotes within string. The echo command uses either double or single quotes to delineate text strings.

If we want to echo a text string on the same line as a command output
```bash
echo -n "Hello I am "
whoami
Hello I am jarvis
```

# Using Variables
---
> Environment Variables

- We can tap into these environment variables from within our scripts by using the environment variable’s name preceded by a dollar sign.
- To display an actual dollar sign, you must precede it with a backslash character.

> User Variables

- User variables can be any text string of up to 20 letters, digits, or an underscore character.
- User variables are case sensitive, so the variable `Var1` is different from the variable `var1`.
- Values are assigned to user variables using an equal sign. No spaces can appear between the variable, the equal sign, and the value.
- Variables deﬁned within the shell script maintain their values throughout the life of the shell script but are deleted when the shell script completes.

# Command Substitution
---
One of the most useful features of shell scripts is the ability to extract information from
the output of a command and assign it to a variable.

There are two ways to assign the output of a command to a variable:
- The back-tick character (\`)
- The $() format
```bash
#!/bin/bash
dt=`date` # is same as
dt1=$(date)
```

```bash
today=$(date +%y%m%d) # display the date as a two-digit year, month, and day
```

# Redirecting Input and Output
---
The bash shell provides a few different operators that allow us to redirect the output of a command to an alternative location.

> Output redirection

The bash shell uses the greater-than symbol (>).
```bash
date > test6
ls -al test6
-rw-r--r-- 1 user user   29 Feb 10 17:56 test6
$ cat test6
Thu Feb 10 17:56:58 EDT 2014
```

The redirect operator created the ﬁle `test6` (using the default umask settings) and redirected the output from the date command to the `test6` ﬁle. If the output ﬁle already
exists, the redirect operator overwrites the existing ﬁle. `>>` appends to the file instead of over-writing.

> Input Redirection

Instead of taking the output of a command and redirecting it to a ﬁle, input redirection takes the content of a ﬁle and redirects it to a command
```bash
wc < test6
	2   11  60
```

# Pipes
---
Sometimes, you need to send the output of one command to the input of another command. This can be done using I/O redirection however pipes provide a efficient way of doing this.

The pipe symbol often looks like a single vertical line in print (|). Don’t think of piping as running two commands back to back. The Linux system actually runs both commands at the same time, linking them together internally in the system. As the ﬁrst command produces output, it’s sent immediately to the second command.


# Performing Math
---
> The `expr` command

```bash
expr ARG1 opr ARG2
```
`opr` can be any of the following `|`, `&`, `<`,`<=`, `=`, `>`, `>=`, `+`, `-`, `*`, `/`, `%`, and so on. But using inside the scripts is somewhat ugly. There is another way to do this.

> Using brackets

In bash, when assigning a mathematical value to a variable, you can enclose the mathematical equation using a dollar sign and square brackets ($[ ]). The bash shell mathematical operators support only integer arithmetic.

> A floating-point solution

The most popular solution uses the built-in bash calculator, called `bc`.
