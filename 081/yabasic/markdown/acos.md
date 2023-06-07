# acos() 

Returns the arcus cosine of its numeric argument.

## Synopsis

```basic
x=acos(angle)
```

## Description

```acos``` is the arcus cosine-function, i.e. the inverse of the [```cos```](cos.html)-function. Or, more elaborate: It Returns the angle (in radians, not degrees!), which, fed to the cosine-function will produce the argument passed to the ```acos```-function.

## Example

```basic
print acos(0.5),acos(cos(pi))
```

This example will print ```1.0472 3.14159``` which are π/3 and π respectively.

## See also

 * [cos](cos.html)
 * [asin](asin.html)
