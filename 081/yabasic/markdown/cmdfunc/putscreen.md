# putscreen

Draw a rectangle of characters into the text terminal.

## Synopsis

```basic
clear screen
…
a$=getscreen$(5,5,10,10)
…
putscreen a$,7,7
```

## Description

The ```putscreen```-command is the counterpart of the [```getscreen$```](getscreen.html)-function. ```putscreen``` requires a string as returned by the [```getscreen$```](getscreen.html)-function. Such a string contains a rectangular detail from the terminal; the ```putscreen```-function puts such a region back into the terminal-window.

Note, that [clear screen](clear-screen.html) must have been called before.

## Example

```basic
clear screen
for a=1 to 200
  print color("red") "Hallo !"; 
  print color("blue") "Welt !";
next a
r$=getscreen$(0,0,20,20)
for x=0 to 60
  putscreen r$,x,0
  sleep 0.1
next x
```

This example prints the string ```"Hallo !Welt !"``` all over the screen and then moves a rectangle from one side to the other.

## See also

 * [getscreen$](getscreen.html)
 * [clear screen](clear-screen.html)
