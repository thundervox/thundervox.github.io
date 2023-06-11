# next

Mark the end of a [```for```](for.html) loop.

## Synopsis

```basic
for a=1 to 10
next a
```

## Description

The ```next```-keyword marks the end of a [```for```](for.html)-loop. All statements up to the ```next```-keyword will be repeated as specified with the [```for```](for.html)-clause. Note, that the name of the variable is optional; so instead of ```next``` a you may write ```next```.

## Example

```basic
for a=1 to 300000
  for b=1 to 21+20*sin(pi*a/20)
    print "*";
  next b
  print
  sleep 0.1
next a
```

This example simply plots a sine-curve until you fall asleep.

## See also

 * [for](for.html)
