# pi

A constant with the value ```3.14159```

## Synopsis

```basic
print pi
```

## Description

```pi``` is ```3.14159265359``` (well at least for yabasic); do not try to assign to pi (e.g. ```pi=22/7```) this would not only be mathematically dubious, but would also result in a syntax error.

## Example

```basic
for a=0 to 180
  print "The sine of ",a," degrees is ",sin(a*pi/180)
next a
```

This program uses pi to transform an angle from degrees into radians.

## See also

 * [euler](euler.html)
