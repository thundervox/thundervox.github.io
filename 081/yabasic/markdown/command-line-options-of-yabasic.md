# Chapter 4. Command line options of yabasic

Here are the options, that yabasic accepts on the command line (both under Unix and Windows).

All the options below may be abbreviated (and one hyphen may be dropped), as long as the abbreviation does not become ambiguous. For example, you may write **-e** instead of **\--execute**.

**\--help** or **-?**

Prints a short help message, which itself describes two further help-options.

**\--version**

Prints the version of yabasic.

**\--infolevel** *INFOLEVEL*

Change the infolevel of yabasic, where *INFOLEVEL* can be one of ```debug```, ```note```, ```warning```, ```error```, ```fatal``` and ```bison``` (the default is ```warning```). This option changes the amount of debugging-information yabasic produces. However, normally only the author of yabasic (*me*!) would want to change this.

**\--execute** *A-PROGRAM-AS-A-SINGLE-STRING*

With this option you may specify some yabasic-code to be executed *right away*. This is useful for very short programs, which you do not want to save to a file. If this option is given, yabasic will not read any code from a file. E.g.

```
yabasic -e 'for a=1 to 10:print a*a:next a'
```

prints the square numbers from 1 to 10.

**\--bind** *NAME-OF-STANDALONE-PROGRAM*

Create a standalone program (whose name is specified by *NAME-OF-STANDALONE-PROGRAM*) from the yabasic-program, that is specified on the command line. See the section about [creating a *standalone*-program]()<sup>**?**</sup> for details.

**\--geometry** +*X-POSITION*+*Y-POSITION*

Sets the position of the graphic window, that is opened by ```open window``` (the size of this window, of course, is specified within the ```open window```-command). An example would be ```-geometry +20+10```, which would place the graphic window 10 pixels below the upper border and 20 pixels right of the left border of the screen. This value cannot be changed, once yabasic has been started.

**-fg** *FOREGROUND-COLOR* or **\--foreground** *FOREGROUND-COLOR*

*Unix only*. Define the foreground color for the graphics-window (that will be opened with [```open window```]()<sup>**?**</sup>). The usual X11 color names, like *red*, *green*, … are accepted. This value cannot be changed, once yabasic has been started.

**-bg** *BACKGROUND-COLOR* or **\--background** *BACKGROUND-COLOR*

*Unix only*. Define the background color for the graphics-window. The usual X11 color names are accepted. This value cannot be changed, once yabasic has been started.

**\--display** *X11-DISPLAY-SPECIFICATION*

*Unix only*. Specify the *display*, where the graphics window of yabasic should appear. Normally this value will be already present within the environment variable ```DISPLAY```.

**\--font** *NAME-OF-FONT*

*Under Unix*. Name of the font, which will be used for text within the graphics window.

**\--font** *NAME-OF-FONT*

*Under Windows*. Name of the font, which will be used for graphic-text; can be any of ```decorative```, ```dontcare```, ```modern```, ```roman```, ```script```, ```swiss```. You may append a fontsize (measured in pixels) to any of those fontnames; for example ```--font swiss30``` chooses a swiss-type font with a size of 30 pixels.

**\--docu** *NAME-OF-A-PROGRAM*

Print the *embedded documentation* of the named program. The embedded documentation of a program consists of all the comments within the program, which start with the special keyword [```doc```]()<sup>**?**</sup>). This documentation can also be seen by choosing the corresponding entry from the context-menu of any yabasic-program.

**\--check**

Check for possible compatibility problems within your yabasic-program. E.g. this option reports, if you are using a function, that has recently changed.

**\--librarypath** *DIRECTORY-WITH-LIBRARIES*

Change the directory, wherein libraries will be searched and imported (with the [```import```]()<sup>**?**</sup>-command). See also [```import```]()<sup>**?**</sup> for more information about the way, libraries are searched.

**\--**

 Do not try to parse any further options; rather pass the subsequent words from the commandline to yabasic.
