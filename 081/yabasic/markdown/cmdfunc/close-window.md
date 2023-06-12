# close window

Close the graphics-window.

## Synopsis

```basic
close window
```

## Description

The ```close window```-command closes the graphics-window, i.e. it makes it disappear from your screen. It includes an implicit [```close printer```](close-printer.html), if a printer has been opened previously.

## Example

```basic
open window 200,200
circle 100,100,50
close window
```

This example will open a window, draw a circle and close the window again; all this without any pause or delay, so the window will be closed before you may regard the circle.

## See also

 * [open window](open-window.html)
