# upper$()

Convert a string to upper case.

## Synopsis

```basic
u$=upper$(a$)
```

## Description

The ```upper$```-function accepts a single string argument and converts it to all upper case.

## Example

```basic
line input "Please enter a sentence without the letter 'e': " l$
p=instr(upper$(l$),"E")
if (p) then
  l$=lower$(l$)
  mid$(l$,p,1)="E"
  print "Hey, you are wrong, see here!"
  print l$
else
  print "Thanks."
endif
```

This program asks for a sentence and marks the first (if any) occurrence of the letter 'e' by converting it to upper case (in contrast to the rest of the sentence, which is converted to lower case).

## See also

 * [lower$](lower.html)
