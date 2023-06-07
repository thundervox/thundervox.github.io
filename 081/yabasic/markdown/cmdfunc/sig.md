# sig()

Return the sign of its argument.

## Synopsis

```basic
a=sig(b)
```

## Description

Return ```+1```, ```-1``` or ```0```, if the single argument is positive, negative or zero.

## Example

```basic
clear screen
dim c$(3):c$(1)="red":c$(2)="white":c$(3)="green"
do
  num=ran(100)-50
  print color(c$(2+sig(num))) num
loop
```

This program prints an infinite sequence of random number; positive numbers are printed in green, negative numbers are printed red (an exact zero would be printed white). (With a little extra work, this program could be easily extended into a brokerage system)

## See also

 * [abs](abs.html)
 * [int](int.html)
 * [frac](frac.html)

