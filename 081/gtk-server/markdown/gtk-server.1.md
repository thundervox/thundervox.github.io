# gtk-server

Section: User Commands (1)
 
## NAME

gtk-server - GUI access for shellscripts and interpreted languages.  

## SYNOPSIS


**gtk-server** *<-stdin> | <-tcp>=host:port[:max] | <-sock>=host:port | <-udp>=host:port | <-fifo>=filename | <-ipc>=number [-log=filename] [-signal=number] [-cfg=filename] [-pre=string] [-post=string] [-handle] [-detach] [-nocreate] [-showconf] [-start=macro] [-init=handshake] [-ssl=[cert.pem]] [-password=passwd] [-ca=cert.pem]*

## DESCRIPTION

The GTK-server is a binary which can be started from a (shell-)script or an interpreted language. It will read the configuration file 'gtk-server.cfg' after which a client script can execute GTK functions. These GTK functions are sent in plain text to the gtk-server, using a 2-way pipe, a named pipe or a TCP or UDP connection.

The GTK-server was inspired by 'dtksh' for the Common Desktop Environment (CDE).  

## ARGUMENTS

The GTK-server must be started with one of the following arguments:

**-stdin**

Start the GTK-server with 2-way pipes. The client script language must start a 2-way pipe to the GTK-server to enable communication. (In KSH and AWK for example, the symbol '|&' is used for this.)

**-tcp=host:port[:max]**

Start the GTK-server as TCP server. The client script language must connect to this host and port. Commonly 'localhost' and a portnumber higher than 1024 are used. The 'max' part determines the maximum amount of client scripts which can connect. If 'max' is omitted only 1 client script may connect.

**-sock=host:port**

Start the GTK-server as TCP client. The client script language acts like a server, sending the commands to the GTK-server.

**-udp=host:port**

Start the GTK-server in UDP mode. The client script must connect to <host> and <port> using the UDP protocol.

**-fifo=<file>**

Start the GTK-server with a named pipe. The pipe is created by the GTK-server automatically and has the name of <file>. When the script is finished the named pipe will be deleted automatically. To avoid the pipe being created automatically, also use the option 'nocreate'.

**-ipc=number**

Start the GTK-server with a message queue. The number must lay within the range from 1 to 65535 and specifies the queue number. When the script is finished the GTK-server will delete the message queue from memory.
After the GTK-server has been started with a message queue, subsequent GTK requests must be sent with the GTK-server binary using the argument 'msg'. The number of the communication channel must be specified, as well as the string to be sent. For example:

**gtk-server -msg=1,gtk_init NULL NULL**

Here a GTK function is sent to communication channel 1. Make sure there is no space between the number, the comma and the string, otherwise the GTK-server will regard these as separate arguments.
Message queues also can be retrieved using the Unix command 'ipcs', and can be deleted using the Unix command 'ipcrm'.


