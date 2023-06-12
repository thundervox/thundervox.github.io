# endif

Ends an [```if```](if.html)-statement.

## Synopsis

```basic
if (…) then
  …
endif
```

## Description

The ```endif```-statement closes (or ends) an [```if```](if.html)-statement.

Note, that ```endif``` may be written in a variety of other ways: ```end if```, ```end-if``` or even [```fi```](fi.html).

The ```endif```-statement must be omitted, if the [```if```](if.html)-statement does not contain the keyword then (see the example below). Such an [```if```](if.html)-statement without endif extends only over a single line.

## Example

```basic
input "A number please: " a
if (a<10) then
  print "Your number is less than 10."
endif

REM  and now without endif 

input "A number please: " a
if (a<10) print "Your number is less than 10."
```

## See also
 * [if](if.html)
