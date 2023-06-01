# The GTK-server Tutorial: a "Hello world" application


## Contents

* [Introduction](#introduction)
* [Chapter 1. Setting up your environment](#chapter-1-setting-up-your-environment)
* [Chapter 2. First steps](#chapter-2-first-steps)
* [Chapter 3. GTK programming - the main window](#chapter-3-gtk-programming---the-main-window)
* [Chapter 4. GTK programming - containers](#chapter-4-gtk-programming---containers)
* [Chapter 5: GTK programming - labels](#chapter-5-gtk-programming---labels)
* [Chapter 6: GTK programming - buttons](#chapter-6-gtk-programming---buttons)
* [Chapter 7. GTK programming - the mainloop](#chapter-7-gtk-programming---the-mainloop)
* [Chapter 8. GTK programming - closing the main window](#chapter-8-gtk-programming---closing-the-main-window)
* [Chapter 9. Using colors](#chapter-9-using-colors)
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

Well, so far so good! We have a start with our AWK script, and we have a first setup of the gtk-server.cfg file. Now, let's go on with the real programming and put the "gtk_init" into our AWK script:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#
BEGIN{

GTK = "gtk-server -stdin"

print "gtk_init NULL NULL" |& GTK; GTK |& getline
```

The line starting with 'print' will actually create a 2-way pipe to the GTK-server. This is a genuine AWK technique. The pipe operator "|&" was borrowed from KSH. It sets up a communication channel on which plain data can be sent and received. As you can see, the AWK script sends the GTK function name as plain text towards the server, and after that, the server will send information back.

This is an important thing to remember: every time information is sent to the GTK-server, the server will send information back! If the GTK function has no returnvalue (like "gtk_init"), the server will return a plain "ok" to the script. If the GTK function was not recognized, the server will return a "-1". Please keep in mind that the GTK-server always will return a string.

Okay, we are ready to create our main window. The GTK function we will use is called "gtk_window_new". This function however will return an identifier referring to the created window. If a GTK function returns an identifier for a widget, this must be defined as WIDGET in the configfile. But also, it has a "GtkWindowType"-argument which is a C typedefinition. How to explain this in our configfile?

The C typedefinitions are a little bit tricky. There are a lot of GTK typedefinitions, and to define all these in the GTK-server would be extremely redundant. The C programming language however uses an internal integer numbering for the typedefinitions. If you look at the typedefinitions for "GtkWindowType", there are 2 types defined: GTK_WINDOW_TOPLEVEL and GTK_WINDOW_POPUP. Now, the C language will refer to the first type with '0' and to the second type with '1'. These are regular integer numbers. In that case, we can define the argument type for "gtk_window_new" as LONG. The gtk-server configfile will now look like this:

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, NONE, WIDGET, 1, LONG
#

```

We will not yet define a callback signal for the window. All right, let's go to the AWK script!

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#

BEGIN{

GTK = "gtk-server -stdin"

print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW
```

You can see that the returnvalue of the GTK function is captured in the variable "WINDOW". Later on, we can use the variable to perform actions on our window. Let's do that right now; let's define a name in the titlebar of our window. The GTK function for this is called "gtk_window_set_title". It has no returnvalue, and it uses 2 arguments: the window of which the title must be set, and the title itself. This is our configfile now:

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, NONE, WIDGET, 1, LONG
FUNCTION_NAME = gtk_window_set_title, NONE, NONE, 2, WIDGET, STRING
#
```

And the AWK script will look like this:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#
BEGIN{

GTK = "gtk-server -stdin"

print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW
print "gtk_window_set_title " WINDOW " \"This is a title\"" |& GTK; GTK |& getline
```

Pretty easy, isn't it?


## Chapter 4. GTK programming - containers

According to the original GTK principles, we must define a container to pack our widgets. It is possible to define the window as a container, but personally, I prefer to use tables. If a table is defined, it is easy to define your widgets using relational coordinates. To create a table on the window, the function "gtk_table_new" must be used. This function returns a widget and uses 3 arguments (we will use no callback signals for the table). The first 2 arguments determine the amount of rows and columns in the table. The third argument is a boolean argument. We can workaround this by using the same trick as we did for the typedefinitions: using '0' for 'false' and '1' for 'true'.

Also, the table must be nailed to the window. This is done with "gtk_container_add". This function uses 2 arguments: the widget (Window) on which the other widget (Table) will be nailed. Our configfile now will look like:

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, NONE, WIDGET, 1, LONG
FUNCTION_NAME = gtk_window_set_title, NONE, NONE, 2, WIDGET, STRING
FUNCTION_NAME = gtk_table_new, NONE, WIDGET, 3, LONG, LONG, LONG
FUNCTION_NAME = gtk_container_add, NONE, NONE, 2, WIDGET, WIDGET
#
```

This is the AWK script:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#

BEGIN{

GTK = "gtk-server -stdin"
print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW
print "gtk_window_set_title " WINDOW " \"This is a title\"" |& GTK; GTK |& getline
print "gtk_table_new 30 30 1" |& GTK; GTK |& getline TABLE
print "gtk_container_add " WINDOW " " TABLE |& GTK; GTK |& getline
```


## Chapter 5: GTK programming - labels

Now, the message "Hello world" must appear in our window. We have to define a label. There is a very convenient GTK function for this: "gtk_label_new", with only 1 argument containing the text to be displayed.

But also, this widget has to be 'packed' onto the table. We will use the "gtk_table_attach_defaults" function. The first argument determines the table we want to use, the second the widget to pack, then the left x and right x coordinate (related to the table) are mentioned, and finally the upper and lower y coordinate are mentioned.

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, NONE, WIDGET, 1, LONG
FUNCTION_NAME = gtk_window_set_title, NONE, NONE, 2, WIDGET, STRING
FUNCTION_NAME = gtk_table_new, NONE, WIDGET, 3, LONG, LONG, LONG
FUNCTION_NAME = gtk_container_add, NONE, NONE, 2, WIDGET, WIDGET
FUNCTION_NAME = gtk_label_new, NONE, WIDGET, 1, STRING
FUNCTION_NAME = gtk_table_attach_defaults, NONE, NONE, 6, WIDGET, WIDGET, LONG, LONG, LONG, LONG
#
```

And the AWK script:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK

#
BEGIN{

GTK = "gtk-server -stdin"

print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW
print "gtk_window_set_title " WINDOW " \"This is a title\"" |& GTK; GTK |& getline
print "gtk_table_new 30 30 1" |& GTK; GTK |& getline TABLE
print "gtk_container_add " WINDOW " " TABLE |& GTK; GTK |& getline
print "gtk_label_new \"Hello world\"" |& GTK; GTK |& getline LABEL
print "gtk_table_attach_defaults " TABLE " " LABEL " 1 29 3 7" |& GTK; GTK |& getline
```


## Chapter 6: GTK programming - buttons

We will also create an "Exit" button. Clicking on this button will exit our "Hello world" application. We must capture the click signal so the AWK script can exit. The GTK function "gtk_button_new_with_label" will create a button, and it also will put some text on it. However, it must be clear that the 'click' signal must be captured.

Well, we are ready now with creating widgets. Finally all widgets must be shown to the world. This is achieved by the GTK function "gtk_widget_show". This function takes only 1 argument, namely, the widget to be shown.

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, NONE, WIDGET, 1, LONG
FUNCTION_NAME = gtk_window_set_title, NONE, NONE, 2, WIDGET, STRING
FUNCTION_NAME = gtk_table_new, NONE, WIDGET, 3, LONG, LONG, LONG
FUNCTION_NAME = gtk_container_add, NONE, NONE, 2, WIDGET, WIDGET
FUNCTION_NAME = gtk_label_new, NONE, WIDGET, 1, STRING
FUNCTION_NAME = gtk_table_attach_defaults, NONE, NONE, 6, WIDGET, WIDGET, LONG, LONG, LONG, LONG
FUNCTION_NAME = gtk_button_new_with_label, clicked, WIDGET, 1, STRING
FUNCTION_NAME = gtk_widget_show, NONE, NONE, 1, WIDGET
```

So the button will return an identifier, and it has 1 argument containing the text to be printed on the button. The callback signal is defined as "clicked". In the GTK documentation all signals which can be emitted by a button are described. The term 'clicked' is a real GTK term for the 'click'-signal. Let's put the button on the window and make it visible. Please note that also the TABLE container must be shown!

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#

BEGIN{

GTK = "gtk-server -stdin"

print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW

print "gtk_window_set_title " WINDOW " \"This is a title\"" |& GTK; GTK |& getline
print "gtk_table_new 30 30 1" |& GTK; GTK |& getline TABLE
print "gtk_container_add " WINDOW " " TABLE |& GTK; GTK |& getline
print "gtk_label_new \"Hello world\"" |& GTK; GTK |& getline LABEL
print "gtk_table_attach_defaults " TABLE " " LABEL " 1 29 3 7" |& GTK; GTK |& getline
print "gtk_button_new_with_label Exit" |& GTK; GTK |& getline BUTTON
print "gtk_table_attach_defaults " TABLE " " BUTTON " 20 28 23 27" |& GTK; GTK |& getline
print "gtk_widget_show " LABEL |& GTK; GTK |& getline
print "gtk_widget_show " BUTTON |& GTK; GTK |& getline
print "gtk_widget_show " TABLE |& GTK; GTK |& getline
print "gtk_widget_show " WINDOW |& GTK; GTK |& getline
```


## Chapter 7. GTK programming - the mainloop

We enter the final stage: defining the mainloop. With GTK you have the possibility to run through all GTK events once. This is performed by the GTK function "gtk_main_iteration". In this iteration the GTK library will check if any event has occured. In our program we want to check if the "click"-signal was emitted by the button. Below the final configfile and AWK program:

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, NONE, WIDGET, 1, LONG
FUNCTION_NAME = gtk_window_set_title, NONE, NONE, 2, WIDGET, STRING
FUNCTION_NAME = gtk_table_new, NONE, WIDGET, 3, LONG, LONG, LONG
FUNCTION_NAME = gtk_container_add, NONE, NONE, 2, WIDGET, WIDGET
FUNCTION_NAME = gtk_label_new, NONE, WIDGET, 1, STRING
FUNCTION_NAME = gtk_table_attach_defaults, NONE, NONE, 6, WIDGET, WIDGET, LONG, LONG, LONG, LONG
FUNCTION_NAME = gtk_button_new_with_label, clicked, WIDGET, 1, STRING
FUNCTION_NAME = gtk_widget_show, NONE, NONE, 1, WIDGET
FUNCTION_NAME = gtk_main_iteration, NONE, WIDGET, 0
```

And the AWK script:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#

BEGIN{

GTK = "gtk-server -stdin"

print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW
print "gtk_window_set_title " WINDOW " \"This is a title\"" |& GTK; GTK |& getline
print "gtk_table_new 30 30 1" |& GTK; GTK |& getline TABLE
print "gtk_container_add " WINDOW " " TABLE |& GTK; GTK |& getline
print "gtk_label_new \"Hello world\"" |& GTK; GTK |& getline LABEL
print "gtk_table_attach_defaults " TABLE " " LABEL " 1 29 3 7" |& GTK; GTK |& getline
print "gtk_button_new_with_label Exit" |& GTK; GTK |& getline BUTTON
print "gtk_table_attach_defaults " TABLE " " BUTTON " 20 28 23 27" |& GTK; GTK |& getline
print "gtk_widget_show " LABEL |& GTK; GTK |& getline
print "gtk_widget_show " BUTTON |& GTK; GTK |& getline
print "gtk_widget_show " TABLE |& GTK; GTK |& getline
print "gtk_widget_show " WINDOW |& GTK; GTK |& getline

EVENT = 0

do {
    print "gtk_main_iteration" |& GTK; GTK |& getline
    print "gtk_server_callback 0" |& GTK; GTK |& getline EVENT

} while (EVENT != BUTTON)

close(GTK)
fflush("")
}
```

Let's take a closer look at the mainloop. We have defined the GTK function "gtk_main_iteration" in the configfile. It will run once, triggered by any GTK event, and update all GTK widgets accordingly. But the function "gtk_server_callback" cannot be found in the configfile! Why not? Because this is an internal function of the GTK-server. It retrieved the last occured signal from the GTK library. If a signal was emitted, the GTK-server returns the widget ID. Else a '0' is returned. In the AWK script above the return value is captured in a variable, which is checked in the 'while' of the mainloop.

If the mainloop closes, the 2-way pipe to the GTK-server will be closed as well. Finally, all AWK buffers are flushed.


## Chapter 8. GTK programming - closing the main window

You may find that it is not possible to close your window with the regular closing facility's of your windowmanager. In Windows you cannot use the cross at the right top of the window. However, this is perfectly ok since the 'delete' signal emitted by the main window is not captured in the AWK script!

In order to close the window in a regular way (without the EXIT button), we must define a callback signal for our main window. The name of the signal when we try to close the window, is called "delete-event". Our configfile must be changed to this:

```bash
#
LIB_NAME = libgtk-x11-2.0.so
#
FUNCTION_NAME = gtk_init, NONE, NONE, 2, NULL, NULL
FUNCTION_NAME = gtk_window_new, delete-event, WIDGET, 1, LONG
FUNCTION_NAME = gtk_window_set_title, NONE, NONE, 2, WIDGET, STRING
FUNCTION_NAME = gtk_table_new, NONE, WIDGET, 3, LONG, LONG, LONG
FUNCTION_NAME = gtk_container_add, NONE, NONE, 2, WIDGET, WIDGET
FUNCTION_NAME = gtk_label_new, NONE, WIDGET, 1, STRING
FUNCTION_NAME = gtk_table_attach_defaults, NONE, NONE, 6, WIDGET, WIDGET, LONG, LONG, LONG, LONG
FUNCTION_NAME = gtk_button_new_with_label, CLICK, WIDGET, 1, STRING
FUNCTION_NAME = gtk_widget_show, NONE, NONE, 1, WIDGET
FUNCTION_NAME = gtk_main_iteration, NONE, WIDGET, 0
```

As you can see, the GTK function "gtk_window_new" is redefined with the callback signal "delete-event". Please make sure you do not use capitals for the GTK signal!

If we run our AWK script now, the main window will listen to the "delete-event" signal. However, we must change our mainloop also, to really exit the application. Below a suggestion on how to do this:

```gawk
#!/usr/bin/gawk -f
#
# AWK Hello world application using GTK
#

BEGIN{

GTK = "gtk-server -stdin"
print "gtk_init NULL NULL" |& GTK; GTK |& getline
print "gtk_window_new 0" |& GTK; GTK |& getline WINDOW
print "gtk_window_set_title " WINDOW " \"This is a title\"" |& GTK; GTK |& getline
print "gtk_table_new 30 30 1" |& GTK; GTK |& getline TABLE
print "gtk_container_add " WINDOW " " TABLE |& GTK; GTK |& getline
print "gtk_label_new \"Hello world\"" |& GTK; GTK |& getline LABEL
print "gtk_table_attach_defaults " TABLE " " LABEL " 1 29 3 7" |& GTK; GTK |& getline
print "gtk_button_new_with_label Exit" |& GTK; GTK |& getline BUTTON
print "gtk_table_attach_defaults " TABLE " " BUTTON " 20 28 23 27" |& GTK; GTK |& getline
print "gtk_widget_show " LABEL |& GTK; GTK |& getline
print "gtk_widget_show " BUTTON |& GTK; GTK |& getline
print "gtk_widget_show " TABLE |& GTK; GTK |& getline
print "gtk_widget_show " WINDOW |& GTK; GTK |& getline

EVENT = 0

do {

    print "gtk_main_iteration" |& GTK; GTK |& getline
    print "gtk_server_callback 0" |& GTK; GTK |& getline EVENT

} while (EVENT != BUTTON && EVENT != WINDOW)

close(GTK)
fflush("")
}
```

## Chapter 9. Using colors

It is also possible to use colors in your application. This might seem strange since the coloring of widgets is a sake of GDK instead of GTK. However, with the GTK-server you can use GTK commands for coloring widgets.

In our example, let's try to color the button. First we have to give this widget a particular name. Let's name it "exitbutton". After the name has been set, the script has to read an external file which contains the color definitions.

