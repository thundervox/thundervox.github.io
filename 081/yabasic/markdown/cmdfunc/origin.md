# origin 

Move the origin of a window.

## Synopsis

```basic
open window 200,200
origin "cc"
```

## Description

The ```origin```-command applies to graphic windows and moves the origin of the coordinate system to one of nine point within the window. The normal position of the origin is in the upper left corner of the window; however in some cases this is inconvenient and moving the origin may save you from subtracting a constant offset from all of your coordinates.

However, you may not move the origin to an arbitrary position; in horizontal position there are only three positions: left, center and right, which are decoded by the letters ```l```, ```c``` and ```r```. In vertical position the allowed positions are top, center and bottom; encoded by the letters ```t```, ```c``` and ```b```. Taking the letters together, you arrive at a string, which might be passed as an argument to the command; e.g. ```"cc"``` or ```"rt"```.

## Example

```basic
100,100
open window 200,200
window origin "cc"
circle 0,0,60
```

This example draws a circle, centered at the center of the window.

## See also

 * [open window](open-window.html)

