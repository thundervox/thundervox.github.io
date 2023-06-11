# mid$()

Return (or *change*) characters from within a string.

## Synopsis

```basic
print mid$(a$,2,1)
print mid$(a$,2)
mid$(a$,5,3)="foo"
mid$(a$,5)="foo"
```

## Description

The ```mid$```-function requires three arguments: a string and two numbers, where the first number specifies a position within the string and the second one gives the number of characters to be returned; if you omit the third argument, the ```mid$```-function returns all characters up to the end of the string.

Note, that you may assign to the ```mid$```-function, i.e. ```mid$``` may appear on the left hand side of an assignment. In this way it is possible to change a part of the variable used within the ```mid$```-function. Note, that that way the *length* of the string cannot be changed, i.e. characters might be overwritten, but not added. For an example see below.

## Example

```basic
input "Please enter a string: " a$
for a=1 to len(a$)
  if (instr("aeiou",lower$(mid$(a$,a,1)))) mid$(a$,a,1)="e"
next a
print "When you turn everything to lower case and"
print "replace every vowel with 'e', your input reads:"
print
print a$
```

This example transforms the input string a bit, using the ```mid$```-function to retrieve a character from within the string as well as to change it.

## See also

 * [left$](left.html)
 * [right$](right.html)
