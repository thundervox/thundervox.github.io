# clear screen

Erases the text window.

## Synopsis

```basic
clear screen
```

## Description

```clear screen``` erases the text window (the window where the output of [```print```](print.html) appears).

It must be issued at least once, before some advanced [```screen```](screen.html)-commands (e.g. ```print at``` or [```inkey$```](inkey.html)) may be called; this requirement is due to some limitations of the ```curses```-library, which is used by yabasic under Unix for some commands.

## Example

```basic
clear screen
print "Please press a key : ";
a$=inkey$
print a$
```

The ```clear screen``` command is essential here; if it would be omitted, yabasic would issue an error (```"need to call 'clear screen' first"```) while trying to execute the inkey$-function.

## See also

 * [inkey$](inkey.html)
 
