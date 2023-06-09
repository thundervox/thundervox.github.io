# close

Close a file, which has been opened before.

## Synopsis

```basic
close filenum
close # filenum
```

## Description

The ```close```-command closes an open file. You should issue this command as soon as you are done with reading from or writing to a file.

## Example

```basic
open "my.data" for reading as 1
input #1 a
print a
close 1
```

This program opens the file ```"my.data"```, reads a number from it, prints this number and closes the file again.

## See also

 * [open](open.html)
