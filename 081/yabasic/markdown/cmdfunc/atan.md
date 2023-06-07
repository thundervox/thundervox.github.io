# atan()

Returns the arctangent of its numeric argument.

## Synopsis

```basic
angle=atan(a,b)
angle=atan(a)
```

## Description

```atan``` is the arctangent-function, i.e. the inverse of the [```tan```](tan.html)-function. Or, more elaborate: It Returns the angle (in radians, not degrees!), which, fed to the ```tan```-function will produce the argument passed to the ```atan```-function.

The ```atan```-function has a second form, which accepts two arguments: ```atan(a,b)``` which is (mostly) equivalent to ```atan(a/b)``` *except* for the fact, that the two-argument-form returns an angle in the range -π to π, whereas the one-argument-form returns an angle in the range -π/2 to π/2. To understand this you have to be good at math.

## Example

```basic
print atan(1),atan(tan(pi)),atan(-0,-1),atan(-0,1)
```

This will print ```0.463648 2.06823e-13 -3.14159 3.14159``` which is π/4, almost 0, -π and π respectively.

## See also

 *  [tan](tan.html)
 *  [sin](sin.html)
