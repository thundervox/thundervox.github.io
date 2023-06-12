# do

Start a (conditionless) ```do-loop```.

## Synopsis

```basic
do 
… 
loop
```

## Description

Starts a loop, which is terminated by ```loop```; everything between ```do``` and ```loop``` will be repeated forever. This loop has no condition, so it is an infinite loop; note however, that a [```break```](break.html)- or [```goto```](goto.html)-statement might be used to leave this loop anytime.

## Example

```basic
do
  a=a+1
  print a
  if (a>100) break
loop
```         

This example prints the numbers between 1 and 101. The [```break```](break.html)-statement is used to leave the loop.

## See also
 * [loop](loop.html)
 * [repeat](repeat.html)
 * [while](while.html)
 * [break](break.html)
 * [goto](goto.html)
