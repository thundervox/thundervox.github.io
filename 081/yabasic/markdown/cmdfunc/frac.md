# frac()

Return the fractional part of its numeric argument.

## Synopsis

```basic
x=frac(y)
```

## Description

The ```frac```-function takes its argument, removes all the digits to the left of the comma and just returns the digits right of the comma, i.e. the fractional part.

Refer to the example to learn how to rewrite ```frac``` by employing the ```int```-function (which is not suggested anyway).

## Example

```basic
for a=1 to 10
  print frac(sqr(a))
  print sqr(a)-int(sqr(a))
next a
```

The example prints the fractional part of the square root of the numbers between 1 and 10. Each result is computed (and printed) twice: Once by employing the frac-function and once by employing the [```int```](int.html)-function.

## See also

 * [int](int.html)
 * [floor](floor.html)
 * [ceil](ceil.html)
 * [round](round.html)
