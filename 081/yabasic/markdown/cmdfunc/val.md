# val()

Converts a string to a number.

## Synopsis

```basic
x=val(x$)
```

## Description

The ```val```-function checks, if the start of its string argument forms a floating point number and then returns this number. The string therefore has to start with digits (only whitespace in front is allowed), otherwise the ```val```-function returns zero.

## Example

```basic
input "Please enter a length, either in inches (in) or centimeters (cm) " l$
if (right$(l$,2)="in") then
  l=val(l$)*2.51
else
  l=val(l$)
print "You have entered ",l,"cm."
```

This example queries for a length and checks, if it has been specified in inches or centimeters. The length is then converted to centimeters.

## See also

 * [str$](str.html)
