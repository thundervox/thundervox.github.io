# The GTK-server Tutorial: a "Hello world" application

## Contents

* [Introduction](#introduction)
* [Chapter 1. Setting up your environment](#chapter-1-setting-up-your-environment)
* [Chapter 2. First steps](#chapter-2-first-steps)
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

During the process of creating the AWK script, also the GTK-server configfile will be created. Every time a GTK function is used, this function must be specified in the configfile as well. But first, let's program a few default AWK lines to get started:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#
BEGIN{

GTK = "gtk-server -stdin"
```

Now, from this piece of code we can see that the interpreter is called in the first line (gawk). Then there are some commentlines starting with a "#", after that the BEGIN rule is defined, and finally the variable GTK is declared as the GTK-server with the stdin argument. It is NOT necessary to have the GTK-server binary in the same directory as your script. The GTK-server will search for the configfile in the "/usr/local/etc" and "/etc" directory. If the configfile isn't available there, the server will exit.

Now, before starting to use the GTK-server, the configfile must be defined. The name of this file MUST be "gtk-server.cfg". There are 3 setting types which must be defined. The first one is "LIB_NAME". You need to specify the actual Shared Object name of your GTK library. Most likely this will be something like "libgtk-1.2.so" or "libgtk-x11-2.0.so". So the first entry in our configfile will look similar to this:

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
```

It is allowed to use "#" in the configfile as well, so you can put your comments there. The next setting we are going to use, is FUNCTION_NAME. In order to use the GTK library, we must initialize first. This is done with the GTK function "gtk_init". Now, we will put this function into our configfile as follows:


```bash
#
LIB_NAME = libgtk-x11-2.0.so
#

FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
#
```

Next to the name of the GTK function, more definitions are encountered. First a 'NONE' is defined. This first NONE defines the callback signal. Callback signals occur when you click with your mouse on a button, for example. The initialization of the GTK library however has no callback signal of itself. The second NONE defines the returnvalue of the "gtk_init" function; it means that the function does not have a return value. Then the number '2', this number defines the amount of arguments to the "gtk_init" function. And finally, the last two definitions specify the type of the arguments. If 'NULL' is defined, it means that the argument has no specific type.

## Chapter 3. GTK programming - the main window

