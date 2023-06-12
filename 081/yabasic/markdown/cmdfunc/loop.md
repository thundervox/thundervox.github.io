# loop

Marks the end of an infinite loop.

## Synopsis

```basic
do
  …
loop
```

## Description

The ```loop```-command marks the ends of a loop (which is started by [```do```](do.html)), wherein all statements within the loop are repeated forever. In this respect the ```do loop```-loop is infinite, however, you may leave it anytime via [```break```](break.html) or [```goto```](goto.html).

## Example

print "Hello, I will throw dice, until I get a 2 ..."

```basic
do
  r=int(ran(6))+1
  print r
  if (r=2) break
loop
```

## See also

 * [do](do.html)
 * [for](for.html)
 * [repeat](repeat.html)
 * [while](while.html)
 * [break](break.html)
