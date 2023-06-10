# break

Breaks out of one or more loops or switch statements.

## Synopsis

```basic
break
break 2
```

## Description

```break``` transfers control immediately outside the enclosing loop or switch statement. This is the preferred way of leaving a such a statement (rather than goto, which is still possible in most cases). An optional digit allows one to break out of multiple levels, e.g. to leave a loop from within a switch statement. Please note, that only a literal (e.g. 2) is allowed at this location.

## Example

```basic
for a=1 to 10
  break
  print "Hi"
next a

while 1
  break
  print "Hi"
wend

repeat
  break
  print "Hi"
until 0

switch 1
case 1:break
case 2:case 3:print "Hi"
end switch
```

This example prints nothing at all, because each of the loops (and the [```switch```](switch.html)-statement) does an immediate ```break``` (before it could print any "Hi").

## See also

 * [for](for.html)
 * [while](while.html)
 * [repeat](repeat.html)
 * [switch](switch.html)
