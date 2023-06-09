# bind()

Binds a yabasic-program and the yabasic-interpreter together into a standalone program.

## Synopsis

```basic
bind("foo.exe")
```

## Description

The ```bind```-command combines your own yabasic-program (plus all the libraries it does ```import```) and the interpreter by copying them into a new file, whose name is passed as an argument. This new program may then be executed on any computer, even if it does not have yabasic installed.

Please see the section about [Creating a *standalone*-program](creating-a-standalone-program.html) for details.

## Example

```basic
if (!peek("isbound")) then
  bind "foo"
  print "Successfully created the standalone executable 'foo' !"
  exit
endif
print "Hello World !"
```

This example creates a standalone program ```foo``` from itself.

## See also

The section about [Creating a *standalone*-program](creating-a-standalone-program.html), the [```peek```](peek.html)-function and the command line [options](command-line-options-of-yabasic.html).
