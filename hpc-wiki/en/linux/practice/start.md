# Getting start with Linux

By following this wiki, you will login to one of the access nodes of the HPC cluster, learn about the Linux shell and issue a very simple Linux command on the virtaul terminal.

## Obtain an user account

Please refer to [this guide](#!cluster_howto/access.md#Obtain_an_user_account).

## SSH login with Putty

Please refer to [this guide](#!cluster_howto/access.md#SSH_login_with_Putty).

## The prompt of the shell

After you login to the access node, the first thing you see is a welcome message together with couple of news messages.  Following the messages are few lines of text look similar to the example below:

```bash
honlee@mentat001:~
999 $
```

Every logged-in users is given a ___shell___ to interact with the system.  The example above is technically called the ___prompt___ of the Linux shell, waiting for your commands to the system. On the prompt, you will type in commands to run programs.  Running programs are usually referred to as ___processes___, and their access to computing resources (CPU, memory, disk and network I/O, etc.) are managed internally by the system.

Note: for the simplicity, we will use the symbol `$` to denote the prompt of the shell.

## Environment variables

Every Linux shell comes with a set of variables that can affect the way running processes will behave. Those variables are called ___environment variables___.

Generally speaking, user needs to set or modify some default environment variables to get a particular program running properly. A very common case is to adjust the `PATH` variable to allow the system to find the location of the program's executable when the program is launched by the user.  Another example is to extend the `LD_LIBRARY_PATH` to include the directory where the dynamic libraries needed for running a program can be found.

In the HPC cluster, a set of environment variables has been prepared for the data analysis software supported in the cluster.  Loading these variables into a shell is also made easy using the [Environment Modules](http://modules.sourceforge.net).  For average users, it's not even necessary to load the variables explicitly as a default set of variables corresponding to commonly used neuroimaging software are loaded automatically upon the user login.  More details about loading software in the HPC cluster is found [here]().

## Knowing who you are in the system

The Linux system is designed to support multiple concurrent users.  Every user has an account (i.e. user id) that is the one you used to login to the access node.  Every user account is associated with at-least one group in the system.  In the HPC cluster at DCCN, the system groups are created in response of the research (i.e. PI) groups. User accounts are associated with groups according to the registration during the check-in procedure.

To know about your user id and the system group you are associated with, simply type `id` followed by pressing the _Return_ key to issue the command on the prompt. For example:

```bash
$ id
uid=10343(honlee) gid=601(tg) groups=601(tg)
```

## Using online manuals

A linux command comes with options for additional functionalities, the online manual provides a handy way to find the supported options of a command.  To access to the online manual of a command, one use the command `man` followed by the command in question.  For example, to get all possible options of the `id` command, one does

```bash
$ man id
``` 
