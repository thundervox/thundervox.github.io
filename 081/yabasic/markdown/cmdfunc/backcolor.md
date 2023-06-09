# color

Change color for background of graphic window.

## Synopsis

```basic
backcolour red,green,blue
backcolour "red,green,blue"
```

## Description

Change the color, that becomes visible, if any portion of the window is erased, e.g. after clear window or clear line. Note however, that parts of the window, that show the old background color will not change.

As with the color-command, the new background color can either be specified as a triple of three numbers or as a single string, that contains those three numbers separated by commas.

Note, that the command backcolor can be written as backcolour too and vice versa.

## Example

```basic
open window 255,255
for x=10 to 235 step 10:for y=10 to 235 step 10
  	backcolour x,y,0
	clear window
	sleep 1
next y:next x
```         

This changes the background colour of the graphic window repeatedly and clears it every time, so that it is filled with the new background colour.

## See also

 * [open window](open-window.html)
 * [color](color.html)
 * [line](line.html)
 * [rectangle](rectangle.html)
 * [triangle](triangle.html)
 * [circle](circle.html)
