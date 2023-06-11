# until

End a ```repeat```-loop.

## Synopsis

```basic
repeat 
  …
until …
```

## Description

The ```until```-keyword ends a loop, which has been introduced by the [```repeat```](repeat.html)-keyword. ```until``` requires an expression (see [here](../conditions-and-expressions.html) for details) as an argument; the loop will continue *until* this condition evaluates to true.

## Example

```basic
c=1
s=1
repeat
  l=c
  s=-(s+sig(s))
  c=c+1/s
  print c
until abs(l-c)<0.000001
```

This program calculates the sequence 1/1-1/2+1/3-1/4+1/5-1/6+1/7-1/8+ … ; please let me know, if you know against which value this converges.

## See also

 * [repeat](repeat.html)
