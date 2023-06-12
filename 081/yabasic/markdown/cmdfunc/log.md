# log()

Compute the natural logarithm.

## Synopsis

```basic
a=log(x)
a=log(x,base)
```

## Description

The ```log```-function computes the logarithm of its first argument. The optional second argument gives the base for the logarithm; if this second argument is omitted, the *euler*-constant 2.71828… will be taken as the base.

## Example

```basic
open window 200,200
for x=10 to 190 step 10:for y=10 to 190 step 10
  r=3*log(1+x,1+y)
  if (r>10) r=10
  if (r<1) r=1
  fill circle x,y,r
next y:next x
```

This draws another nice plot.

## See also

* [exp](exp.html)
