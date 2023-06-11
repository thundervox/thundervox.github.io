# or 

Logical or, used in conditions.

## Synopsis

```basic
if a or b …
while a or b …
```

## Description

Used in conditions (e.g within [```if```](if.html) or [```while```](while.html)) to join two expressions. Returns ```true```, if either its left or its right or both arguments are ```true```; returns ```false``` otherwise.

## Example

```basic
input "Please enter a number"
if (a>9 or a<1) print "a is not between 1 and 9"
```

## See also

 * [and](and.html)
 * [bitnot](bitnot.html)
 
