# The GTK-server Tutorial: a "Hello world" application

## Contents

* [Introduction](#introduction)
* Chapter 1. Setting up your environment
* Chapter 2. First steps
* Chapter 3. GTK programming - the main window
* Chapter 4. GTK programming - containers.
* Chapter 5: GTK programming - labels
* Chapter 6: GTK programming - buttons
* Chapter 7. GTK programming - the mainloop
* Chapter 8. GTK programming - closing the main window
* Chapter 9. Using colors
* Chapter 10. Connecting to the GTK-server with TCP or UDP
* Chapter 11. Connecting to the GTK-server with FIFO
* Chapter 12. Logging

## Introduction

In this tutorial we will create a simple window containing the message "Hello world!". We will mainly be using GNU AWK to do that. Basic knowledge of the AWK script language is recommended. If you are unknown to AWK, please consult the excellent GNU AWK manual at [https://www.gnu.org/software/gawk/manual/gawk.html](https://www.gnu.org/software/gawk/manual/gawk.html). Also, this tutorial will focus on the Linux operating system.


# Chapter 1. Setting up your environment

Before starting to use the GTK-server, you have to check your environment variables. AWK will be the main script language in this tutorial, and the AWK script will invoke the GTK-server with the argument 'stdin'. Now, in order for the GTK widgets to be displayed correctly, it is necessary to set your language environment, since the GTK library will use this setting to display it's widgets. You can use the variable LC_ALL to accomplish this. To find out what the current settings are of your environment variables, you can use the command 'set' (BASH, or 'setenv' for CSHELL). This command will list all your variables. On my system, LC_ALL is put to Dutch. In the Linux BASH shell, perform:

```bash
export LC_ALL=nl_NL
```

to set the variable. But this is not all. Also the library path should be set. It must point to the X11R6 library's. This is needed to display text entry widgets for example. In the BASH shell, make sure that the LD_LIBRARY_PATH is set:

```bash
export LD_LIBRARY_PATH=/usr/X11R6/lib
```

Or if this environment variable already has some other value:

```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/X11R6/lib
```

Now your shell environment is setup properly for scripts using the GTK-server with 'stdin'.


## Chapter 2. First steps

