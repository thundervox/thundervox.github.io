# dec()

Convert a base 2 or base 16 number into decimal form.

## Synopsis

```basic
a=dec(number$)
a=dec(number$,base)
```

## Description

The ```dec```-function takes the string-representation of a base-2 or base-16 (which is the default) number and converts it into a decimal number. The optional second argument (```base```) might be used to specify a base other than 16. However, currently only base 2 or base 16 are supported. Please note, that for base 16 and 2 you may write literals in the usual way, by preceding them with ```0x``` or ```0b``` respectively, e.g. like

```basic
print 0xff + 0b11
```

; this may save you from applying the ```dec``` altogether.

## Example

```basic
input "Please enter a binary number: " a$
print a$," is ",dec(a$)
```

## See also

 * [bin$](bin.html)
 * [hex$](hex.html)
 * [numbers with base 2 or 16](numbers-with-base-2-or-16.md)

