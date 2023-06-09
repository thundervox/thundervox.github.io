# at()

Can be used in the ```print```-command to place the output at a specified position.

## Synopsis

```basic
clear screen
…
print at(a,b)
print @(a,b)
```

## Description

The ```at```-clause takes two numeric arguments (e.g. ```at(2,3)```) and can be inserted after the ```print```-keyword. ```at()``` can be used only if [clear screen](clear-screen.html) has been executed at least once within the program (otherwise you will get an error).

The two numeric arguments of the ```at```-function may range from 0 to the width of your terminal minus 1, and from 0 to the height of your terminal minus 1; if any argument exceeds these values, it will be truncated accordingly. However, yabasic has no influence on the size of your terminal (80x25 is a common, but not mandatory), the size of your terminal and the maximum values acceptable within the at-clause may vary. To get the size of your terminal you may use the [```peek```](peek.html)-function: ```peek("screenwidth")``` returns the width of your terminal and ```peek("screenheight")``` its height.

## Example

```basic
clear screen
maxx=peek("screenwidth")-1:maxy=peek("screenheight")-1
for x=0 to maxx
  print at(x,maxy*(0.5+sin(2*pi*x/maxx)/2)) "*"
next x
```
 
This example plots a full period of the sine-function across the screen.

## See also

 * [print](print.html)
 * [clear screen](clear-screen.html)
 * [color](color.html)
