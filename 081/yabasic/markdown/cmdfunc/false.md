# false

A constant with the value of 0.

## Synopsis

```basic
okay=false
```

## Description

The constant ```false``` can be assigned to variables which later appear in conditions (e.g. within an [```if```](if.html)-statement.

```false``` may also be written as ```FALSE``` or even ```FaLsE```.

## Example

```basic
input "Please enter a number between 1 and 10: " a
if (check_input(a)) print "Okay"

sub check_input(x)
  if (x>10 or x<1) return false
  return true
end sub
```

The subroutine ```check_input``` checks its argument and returns ```true``` or ```false``` according to the outcome of the check.

## See also

 * [true](true.html)
