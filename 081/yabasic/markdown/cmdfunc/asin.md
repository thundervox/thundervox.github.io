# asin()

Returns the arcus sine of its numeric argument.

## Synopsis

```basic
angle=asin(x)
```

## Description

```asin``` is the arcus sine-function, i.e. the inverse of the [```sin```](sin.html)-function. Or, more elaborate: It Returns the angle (in radians, not degrees!), which, fed to the sine-function will produce the argument passed to the ```asin```-function.

## Example

```basic
print asin(0.5),asin(sin(pi))
```

This will print ```0.523599 -2.06823e-13``` which is π/6 and almost 0 respectively.

## See also

 * [sin](sin.html)
 * [acos](acos.html)

