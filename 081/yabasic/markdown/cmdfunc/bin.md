# bin$()

Converts a number into a sequence of binary digits.

Synopsis

```basic
hexadecimal$=bin$(decimal)
```

## Description

The ```bin$```-function takes a single numeric argument an converts it into a string of binary digits (i.e. zeroes and ones). If you pass a negative number to ```bin$```, the resulting string will be preceded by a '-'.

If you want to convert the other way around (i.e. from binary to decimal) you may use the [```dec```](dec.html)-function.

## Example

```basic
for a=1 to 100
  print bin$(a)
next a
```

This example prints the binary representation of all digits between 1 and 100.

## See also

 * [hex$](hex.html)
 * [dec](dec.html)
 * [numbers with base 2 or 16](numbers-with-base-2-or-16.html)
