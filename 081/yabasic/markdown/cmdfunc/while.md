# while

Start a ```while```-loop.

## Synopsis

```basic
while …
  …
wend
```

## Description

The ```while```-keyword starts a ```while```-loop, i.e. a loop that is executed as long as the condition (which is specified after the keyword ```while```) evaluates to ```true```.

Note, that the body of such a ```while```-loop will not be executed at all, if the condition following the ```while```-keyword is not ```true``` initially.

If you want to leave the loop prematurely, you may use the [```break```](break.html)-statement.

## Example

```basic
open #1,"foo"
while !eof(1)
  line input #1 a$
  print a$
wend
```

This program reads the file foo and prints it line by line.

## See also

 * [until](until.html)
 * [break](break.html)
 * [wend](wend.html)
 * [do](do.html)
