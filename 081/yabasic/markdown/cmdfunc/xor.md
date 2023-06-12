# xor()

Compute the exclusive or.

## Synopsis

```basic
x=xor(a,b)
```

## Description

The ```xor```-function computes the bitwise *exclusive or* of its two numeric arguments. To understand the result, both arguments should be viewed as binary numbers (i.e. a sequence of digits 0 and 1); a bit of the result will then be 1, if exactly one argument has a 1 and the other has a 0 at this position in their binary representation.

Note, that both arguments are silently converted to integer values and that negative numbers have their own binary representation and may lead to unexpected results when passed to [```and```](and.html).

## Example

```basic
print xor(7,4)
```

This will print 3. This result is obvious, if you note, that the binary representation of 7 and 4 are 111 and 100 respectively; this will yield 011 in binary representation or 2 as decimal.

The [```eor```](eor.html)-function is the same as the ```xor```-function; both are synonymous; however they have each their own description, so you may check out the entry of [```eor```](eor.html) for a slightly different view.

## See also

 * [and](and.html)
 * [or](or.html)
 * [eor](eor.html)
 * [bitnot](bitnot.html)
