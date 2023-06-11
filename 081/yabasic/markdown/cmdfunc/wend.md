# wend

End a [```while```](while.html)-loop.

## Synopsis

```basic
while a<b
  …
wend
```

## Description

The ```wend```-keyword marks the end of a [```while```](while.html)-loop. Please see the [```while```](while.html)-keyword for more details.

```wend``` can be written as ```end while``` or even ```end-while```.

## Example

```basic
line input "Please enter a sentence: " a$
p=instr(a$,"e")
while p
  mid$(a$,p,1)="E"
  p=instr(a$,"e")
wend
print a$
```

This example reads a sentence and converts every occurrence of the letter e into uppercase (E).

## See also

 * [```while```](while.html)
