# exit

Terminate your program.

## Synopsis

```basic
exit
exit 1
```

## Description

Terminate your program and return any given value to the operating system. ```exit``` is similar to [```end```](end.html), but it will terminate your program immediately, no matter what.

## Example

```basic
print "Do you want to continue ?"
input "Please answer y(es) or n(o): " a$
if (lower$(left$(a$,1))="n") exit 1
```

## See also

 * [end](end.html)
