# read

Read data from ```data```-statements.

## Synopsis

```basic
read a$,a
…
data "Hello !",7
```

## Description

The ```read```-statement retrieves literal data, which is stored within [```data```](data.html)-statements elsewhere in your program.

## Example

```basic
read num
dim col$(num)
for a=1 to num:read col$(a):next a
clear screen
print "These are the colours known to yabasic:\n"
for a=1 to num
  print colour(col$(a)) col$(a)
next a

data 8,"black","white","red","blue"
data "green","yellow","cyan","magenta"
```

This program prints the names of the colors known to yabasic in those very colors.

## See also

 * [data](data.html)
 * [restore](restore.html)
