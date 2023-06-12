# sin()

Return the sine of its single argument.

## Synopsis

```basic
y=sin(angle)
```

## Description

The ```sin```-function expects an angle (in radians, *not* degrees) and returns its sine.

## Example

```basic
open window 200,200
new curve
for phi=0 to 2*pi step 0.1
  line to 100+90*sin(phi),100+90*cos(phi)
next phi
close curve
```

This program draws a circle (ignoring the existence of the [```circle```](circle.html)-command).

## See also

 * [asin](asin.html)
 * [cos](cos.html)
