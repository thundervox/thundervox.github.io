# 2. The yabasic-program under Windows

 * [Starting yabasic](#starting-yabasic)
 * [Options](#options)
 * [The context Menu](#the-context-menu)

## Starting yabasic

Once, yabasic has been set up correctly, there are three ways to start it:

1. *Right click on your desktop:* The desktop menu appears with a submenu named *new*. From this submenu choose yabasic. This will create a new icon on your desktop. If you right click on this icon, its [context menu](#the-context-menu) will appear; choose Execute to execute the program.
2. As a variant of the way described above, you may simply create a file with the ending *```.yab```* (e.g. with your favorite editor). Everything else then works as described above.
3. *From the start-menu:* Choose yabasic from your start-menu. A console-window will open and you will be asked to type in your program. Once you are finished, you need to type ```return``` twice, and yabasic will parse and execute your program.

### Note

This is *not* the preferred way of starting yabasic ! Simply because the program, that you have typed, *can not be saved* and will be lost inevitably ! There is no such thing as a ```save```-command and therefore no way to conserve the program, that you have typed. This mode is only intended for quick hacks, and short programs.

## Options

Under Windows yabasic will mostly be invoked by double-clicking on an appropriate icon; this way you do not have a chance to specify any of the command line options below. However, advanced users may change the librarypath in the registry, which has the same effect as specifying it as an option on the command line.

See [the chapter on options]()<sup>**?**</sup> for a complete list of all options, either on Unix or Windows.

### The context Menu

Like every other icon under Windows, the icon of every yabasic-program has a context menu offering the most frequent operations, that may be applied to a yabasic-program.

**Execute**

This will invoke yabasic to execute your program. The same happens, if you *double click* on the icon.

**Edit**

notepad will be invoked, allowing you to edit your program.

**View docu**

This will present the embedded documentation of your program. Embedded documentation is created with the special comment [doc]()<sup>**?**</sup>.
