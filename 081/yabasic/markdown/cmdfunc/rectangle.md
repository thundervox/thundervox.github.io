# rectangle

Draw a rectangle.

## Synopsis

```basic
open window 100,100
rectangle 10,10 to 90,90
rectangle 20,20,80,80
rect 20,20,80,80
box 30,30,70,70
clear rectangle 30,30,70,70
fill rectangle 40,40,60,60
clear fill rectangle 60,60,40,40
```

## Description

The ```rectangle```-command (also known as ```box``` or ```rect```, for short) draws a rectangle; it accepts four parameters: The x- and y-coordinates of two facing corners of the rectangle. With the optional clauses ```clear``` and ```fill``` (which may appear together and in any sequence) the rectangle can be cleared and filled respectively.

## Example

```basic
open window 200,200
c=1
do 
  for phi=0 to pi step 0.1
    if (c) then 
      rectangle 100+100*sin(phi),100+100*cos(phi) to 100-100*sin(phi),100-100*cos(phi)
    else 
      clear rectangle 100+100*sin(phi),100+100*cos(phi) to 100-100*sin(phi),100-100*cos(phi)
    endif
    sleep 0.1
  next phi
  c=not c
loop
```

This example draws a nice animated pattern; watch it for a couple of hours, to see how it develops.

## See also

 * [open window](open-window.html)
 * [open printer](open-printer.html)
 * [line](line.html)
 * [circle](circle.html)
 * [triangle](triangle.html)
