# reverse

Print reverse (background and foreground colors exchanged).

## Synopsis

```basic
clear screen
…
print reverse "foo"
```

## Description

```reverse``` may be used to [```print```](print.html) text in reverse. ```reverse``` is not a separate command, but part of the [```print```](print.html)-command; it may be included just after the [```print```](print.html) and can only be issued once that [```clear screen```](clear-screen.html) has been issued.

## Example

```basic
clear screen

print "1 ";
c=3
do
  prim=true
  for a=2 to sqrt(c)
    if (frac(c/a)=0) then
      prim=false
      break
    endif
  next a
  if (prim) then
    print
    print reverse c;
  else
    print c;
  endif
  print " ";
  c=c+1
loop
```
          

This program prints numbers from 1 on and marks each prime number in reverse.

## See also

 * [at](at.html)
 * [print color](print-color.html)
 * [print](print.html)
 * [clear screen](clear-screen.html)
