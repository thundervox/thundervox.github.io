# case

Mark the different cases within a [switch](switch.html)-statement.

## Synopsis

```basic
switch a
  case 1
  case 2
  …
end switch

…

switch a$
  case "a"
  case "b"
  …
end switch
```

## Description

Please see the [```switch```](switch.html)-statement.

## Example

```basic
input a
switch(a)
  case 1:print "one":break
  case 2:print "two":break
  default:print "more"
end switch
```

Depending on your input (a number is expected) this code will print ```one``` or ```two``` or otherwise ```more```.

## See also

 * [switch](switch.html)
