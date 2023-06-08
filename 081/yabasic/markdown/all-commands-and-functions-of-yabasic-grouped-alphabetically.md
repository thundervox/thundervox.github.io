# Chapter 7. All commands and functions of yabasic grouped alphabetically

## A

abs() — returns the absolute value of its numeric argument

acos() — returns the arcus cosine of its numeric argument

and — logical and, used in conditions

and() — the bitwise arithmetic and

arraydim() — returns the dimension of the array, which is passed as an array reference

arraysize() — returns the size of a dimension of an array

asc() — accepts a string and returns the position of its first character within the ascii charset

asin() — returns the arcus sine of its numeric argument

at() — can be used in the print-command to place the output at a specified position

atan() — returns the arctangent of its numeric argument


## B

backcolor — change color for background of graphic window

beep — ring the bell within your computer; a synonym for bell

bell — ring the bell within your computer (just as beep)

bin$() — converts a number into a sequence of binary digits

bind() — binds a yabasic-program and the yabasic-interpreter together into a standalone program

bitnot() — the bitwise arithmetic not

box — draw a rectangle. A synonym for rectangle

break — breaks out of one or more loops or switch statements


## C

case — mark the different cases within a switch-statement

ceil() — compute the ceiling for its (float) argument

chomp$() — remove a single trailing newline from its string-argument; if the string does not end in a newline, the string is returned unchanged

chr$() — accepts a number and returns the character at this position within the ascii charset

circle — draws a circle in the graphic-window

clear — erase circles, rectangles or triangles

clear screen — erases the text window

clear window — clear the graphic window and begin a new page, if printing is under way

close — close a file, which has been opened before

close curve — close a curve, that has been drawn by the line-command

close printer — stops printing of graphics

close window — close the graphics-window

color — change color for any subsequent drawing-command

compile — compile a string with yabasic-code on the fly

continue — start the next iteration of a for-, do-, repeat- or while-loop

cos() — return the cosine of its single argument


## D

data — introduces a list of data-items

date$ — returns a string with various components of the current date

dec() — convert a base 2 or base 16 number into decimal form

default — mark the default-branch within a switch-statement

dim — create an array prior to its first use

do — start a (conditionless) do-loop

doc — special comment, which might be retrieved by the program itself

docu$ — special array, containing the contents of all docu-statement within the program

dot — draw a dot in the graphic-window


## E

else — mark an alternative within an if-statement

elsif — starts an alternate condition within an if-statement

end — terminate your program

endif — ends an if-statement

end sub — ends a subroutine definition

eof — check, if an open file contains data

eor() — compute the bitwise exclusive or of its two arguments

error — raise an error and terminate your program

euler — another name for the constant 2.71828182864

eval() — compile and execute a single numeric expression

eval$() — compile and execute a single string-expression

execute() — execute a user defined subroutine, which must return a number

execute$() — execute a user defined subroutine, which must return a string

exit — terminate your program

exp() — compute the exponential function of its single argument

export — mark a function as globally visible


## F

false — a constant with the value of 0

fi — another name for endif

fill — draw a filled circles, rectangles or triangles

floor() — compute the floor for its (float) argument

for — starts a for-loop

foreign_buffer_alloc$() — Create a new buffer for use in a foreign function call

foreign_buffer_dump$() — return the content of a buffer as a hex-encoded string

foreign_buffer_free — free a foreign buffer

foreign_buffer_get() — extract a number from a foreign buffer

foreign_buffer_get$() — extract a string from a foreign buffer

foreign_buffer_get_buffer$() — take a buffer and construct a handle to a second buffer from its content

foreign_buffer_set — store a given value within a buffer

foreign_buffer_set_buffer — store a pointer to one buffer within another buffer

foreign_buffer_size() — return the size of the foreign buffer

foreign_function_call() — call a function (returning a number) from a non-yabasic library or dll

foreign_function_call$() — call a function (returning a string or a buffer) from a non-yabasic library or dll

foreign_function_size() — return the size of one of the types available for foreign function calls

frnbf_ and frnfn_ — Abbreviations for foreign_buffer_ and foreign_function_

frac() — return the fractional part of its numeric argument


## G

getbit$() — return a string representing the bit pattern of a rectangle within the graphic window

getscreen$() — returns a string representing a rectangular section of the text terminal

glob() — check if a string matches a simple pattern

gosub — continue execution at another point within your program (and return later)

goto — continue execution at another point within your program (and never come back)


## H

hex$() — convert a number into hexadecimal


## I

if — evaluate a condition and execute statements or not, depending on the result

import — import a library

inkey$ — wait, until a key is pressed

input — read input from the user (or from a file) and assign it to a variable

instr() — searches its second argument within the first; returns its position if found

int() — return the integer part of its single numeric argument


## J

Nothing.


## K

Nothing.


## L

label — mark a specific location within your program for goto, gosub or restore

left$() — return (or change) left end of a string

len() — return the length of a string

line — draw a line

line input — read in a whole line of text and assign it to a variable

local — mark a variable as local to a subroutine

log() — compute the natural logarithm

loop — marks the end of an infinite loop

lower$() — convert a string to lower case

ltrim$() — trim spaces at the left end of a string


## M

max() — return the larger of its two arguments

mid$() — return (or change) characters from within a string

min() — return the smaller of its two arguments

mod — compute the remainder of a division

mouseb — extract the state of the mousebuttons from a string returned by inkey$

mousemod — return the state of the modifier keys during a mouseclick

mousex — return the x-position of a mouseclick

mousey — return the y-position of a mouseclick


## N

new curve — start a new curve, that will be drawn with the line-command

next — mark the end of a for loop

not — negate a logical expression; can be written as !

numparams — return the number of parameters, that have been passed to a subroutine
