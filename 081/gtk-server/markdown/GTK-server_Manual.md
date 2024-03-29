# The GTK-server Quickstart Manual

## 1. The GTK-server binary

This binary tries to open the GTK library on your system. It will look for a GTK library mentioned in the ```gtk-server.cfg``` file. For Windows the GTK DLL is provided in a separate installation package.

Both the Linux version and the Windows version of the GTK-server support communication by a 2-way pipe, named pipe, TCP and UDP. In case of a 2-way pipe, the GTK-server must be started with the argument ```stdin```. In case of a named pipe, the GTK-server must be started with the argument ```fifo```, after which the name of the pipe must be mentioned. In Windows, the name of the named pipe can be omitted; the GTK-server will setup 2 independent pipes, with the predefined names **\\.\pipe\out** and **\\.\pipe\in**. Finally, to enable TCP or UDP communication, the argument must be of the format ```<-tcp=ipaddress:port>``` or ```<-udp= ipaddress:port>```.

Only the Linux version in TCP mode supports multiple connections to one server. To enable this feature, start the GTK-server with the argument ```<-tcp=ipaddress:port:max>```, where ``max`` determines the maximum amount of clients which may connect. If the ```max``` argument is omitted, only one program can connect. In case of Win32 however, the ```max``` argument cannot be used; here it is always necessary to start a separate server for each client program.

If the last argument is ```-log=file.txt```, the GTK-server will produce a logfile with the title ```file.txt```. Any name can be used here, of course. This logfile will contain the strings which were received by the GTK-server, and the responses of the GTK-server to those strings. This is how your script can be checked for GTK errors.

## 2. The GTK-server configfile

In the config file you have to describe the GTK function you want to invoke. Entry's starting with a ```#``` are skipped. You can use the ```#``` to put comments in your config file. Every GTK function has specific properties. Let's take a look at an example:

```bash
FUNCTION_NAME = gtk_toggle_button_new_with_label, clicked, WIDGET, 1, STRING
```

In this line, the GTK function **gtk_toggle_button_new_with_label** is described. (To find out what the properties are for GTK functions, consult the GTK documentation at [https://www.gtk.org/](https://www.gtk.org/)) The next argument describes the type of callback for this widget. A callback is a signal to which the GTK library has to listen. In this case, the toggle button by default will respond to a ```clicked``` signal. This signal occurs when you click with your mouse on this button. Remember, except for the names of the GTK-functions and signals you have to use capitals here!

After the callback signal you have to enter which value is expected back from the GTK function (the returnvalue). In the example above, a widget will be returned to the script. Other returnvalues are ```STRING```, ```BOOL```, ```LONG```, ```FLOAT``` and ```NONE```.Using Glade XML files

After that, you have to specify the amount of arguments needed for this GTK function. In our example only one argument is expected. The type of argument here is ```STRING```. Other argument types are ```LONG```, ```WIDGET```, ```FLOAT```, ```DOUBLE```, ```BASE64``` and ```NULL```. So for each argument you have to declare the type - in the right order! In case of 3 arguments take care that the order you mention is the same as the real order for the GTK-function.

## 3. Catching callback signals

To catch a callback signal from a widget, an internal GTK-server function must be used. The name of the function is ```gtk_server_callback```. This function takes only one argument, a ```0```, ```1``` or a ```2```. Instead of the ```1``` also the word 'wait' can be used, and instead of ```2``` the word ```update``` can be used. The function checks if the userinterface has received a callback signal.

If the argument to ```gtk_server_callback``` is ```2``` then the GTK-server will update all events waiting in the queue and check if there is a callback waiting. With this argument, ```gtk_server_callback``` returns immediately. If there is no callback, a ```0``` is returned, else the widgetID is returned. If the argument is ```1``` the GTK-server will update all events in the queue and wait until an event has occured. Only then ```gtk_server_callback``` returns, with the widgetID on which the signal took place. Finally, if the argument is ```0``` the function will not update the userinterface, but it will only check on an event and return immediately. In this case, the client program has to take care of updating the userinterface by itself - this is sometimes necessary when it needs to wait for other events (like network events) instead of GUI events.

So, if it must be checked in KSH whether or not a toggle button has emitted a ```click``` signal, this can be stated as:

```bash
print -p "gtk_server_callback wait"; read -p EVENT
if [ EVENT -eq BUTTON ]
then
    print "Mouse button pressed!"
fi
```

In the above code, the call will return the widget ID in case an event has occured. Else it will wait. The result will be put into the variable **EVENT**. This result can be compared with existing widget ID's to take appropriate action.

Apart from the default callback signal in the ```gtk-server.cfg``` file, it is also possible to connect a signal manually to a widget. For this the function ```gtk_server_connect``` can be used. This function takes 3 arguments: the widget ID, the signal name and a string to identify the signal. For example:

```bash
print -p "gtk_server_connect BUTTON enter hello"; read -p RESULT
print -p "gtk_server_callback wait"; read -p EVENT
if [ EVENT -eq "hello" ]
then
    print "Mouse entered button region!"
fi
```

Please keep in mind that the GTK-server always returns it's data as a string. In order to use the returned result as a number, some languages (like Scriptbasic) need a typecast.

## 4. Using Glade XML files

If you have designed a user interface with Glade, the GTK-server can read the resulting XML file and realize the interface. First point to the location of the XML file:

```bash
print -p "glade_xml_new mygui.glade $NULL $NULL"; read -p XML
```

Then query Glade for the widgetID which can be used in the mainloop. The names of all widgets are mentioned in the Glade XML file:

```bash
print -p "glade_xml_get_widget $XML nameofwidget"; read -p WIDGET
```

From here you can setup your program in a regular way, using the widgetID to connect signals and catch them in your mainloop.

---
Copyright© December 2003 - December 2008, Peter van Eerten  -  https://www.gtk-server.org/
