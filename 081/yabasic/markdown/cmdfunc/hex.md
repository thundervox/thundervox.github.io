# hex$()

Convert a number into hexadecimal.

## Synopsis

```basic
print hex$(foo)
```

## Description

The ```hex$```-function converts a number into a string with its hexadecimal representation. ```hex$``` is the inverse of the ```dec```-function.

## Example

```basic
open 1,"foo"
while !eof(1)
  print right$("0"+hex$(peek(1)),2)," ";
  i=i+1
  if (mod(i,10)=0) print
end while
print
```

This program reads the file ```foo``` and prints its output as a *hex*-dump using the ```hex```-function.

## See also

 * [decbin](decbin.html)
 * [numbers with base 2 or 16](../numbers-with-base-2-or-16.html)

