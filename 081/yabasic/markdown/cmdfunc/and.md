# and

Logical and, used in conditions.

## Synopsis
```basic
if a and b …
while a and b …
```

## Description

Used in conditions (e.g within [if](if.html), [while](while.html) or [until](until.html)) to join two expressions. Returns true, if and only if its left and right argument are both ```true``` and ```false``` otherwise.

Note, that [*logical shortcuts*](logical-shortcuts.html) may take place.

## Example

```basic
input "Please enter a number" a
if (a>=1 and a<=9) print "your input is between 1 and 9"
```
          
## See also
 * [or](or.html)
 * [not](not.html)
