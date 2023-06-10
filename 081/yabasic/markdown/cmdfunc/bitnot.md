# bitnot()

The bitwise arithmetic ```not```.

## Synopsis

```basic
x=bitnot(a)
```

## Description

This function is used to compute the *bitwise not* of its single argument. The argument is treated as binary number (i.e. a sequence of digits 0 and 1); a bit of the resulting value will be 1, if the argument has a 0 at this position in its binary representation; if the bit in the argument is 1, the bit in the result will be 0.

Note, that its argument is silently converted to a positive integer value and that negative numbers have their own binary representation and may lead to unexpected results when passed to ```bitnot```.

A note on naming: This one-argument-function is named ```bitnot``` to distinguish it from the one-argument-function [```not```](not.html), which operates on *logical* expressions. For the similar functions ```and``` and ```or``` this distinction between *logical* and *bitwise* function is done implicitly through the number of arguments (1 and 2, respectively).

## Example

```basic
print bin$(not(17))
```

This will print ```11111111111111111111111111101110```. This result is clear, if you note, that the binary representation of 17 is 10001, which inverted will give the long binary number given before.

## See also

 * [or()](or2.html)
 * [eor()](eor.html)
 * [and()](and2.html)

