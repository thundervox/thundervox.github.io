# and()

The bitwise arithmetic ```and```

## Synopsis

```basic
x=and(a,b)
```

## Description

Used to compute the bitwise and of both its argument. Both arguments are treated as binary numbers (i.e. a sequence of digits 0 and 1); a bit of the resulting value will then be 1, if both arguments have a 1 at this position in their binary representation.

Note, that both arguments are silently converted to integer values and that negative numbers have their own binary representation and may lead to unexpected results when passed to ```and```.

## Example

```basic
print and(6,3)
```

This will print ```2```. This result is clear, if you note, that the binary representation of 6 and 3 are 110 and 011 respectively; this will yield 010 in binary representation or 2 as decimal.

## See also

 * [or](or2.html)
 * [eor](eor.html)
 * [bitnot](bitnot.html)
