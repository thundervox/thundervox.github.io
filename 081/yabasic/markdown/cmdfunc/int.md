# int()

Return the integer part of its single numeric argument.

## Synopsis

```basic
print int(a)
```

## Description

The ```int```-function returns only the digits before the comma; ```int(2.5)``` returns ```2``` and ```int(-2.3)``` returns ```-2```.

## Example

```basic
input "Please enter a whole number between 1 and 10: " a
if (a=int(a) and a>=1 and a<=10) then
  print "Thanx !"
else
  print "Never mind ..."
endif
```

## See also

 * [frac](frac.html)
 * [floor](floor.html)
 * [ceil](ceil.html)
 * [round](round.html)
