# end sub

Ends a subroutine definition.

## Synopsis

```basic
sub foo(…) 
  …
end sub
```

## Description

Marks the end of a subroutine-definition (which starts with the [```sub```](sub.html)-keyword). The whole concept of subroutines is explained within the entry for [```sub```](sub.html).

## Example

```basic
print foo(3)
sub foo(a)
  return a*2
end sub
```

This program prints out ```6```. The subroutine ```foo``` simply returns twice its argument.

## See also

 * [sub](sub.html)
