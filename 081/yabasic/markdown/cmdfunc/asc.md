# asc()

Accepts a string and returns the position of its first character within the ascii charset.

## Synopsis

```basic
a=asc(char$)
```

## Description

The ```asc```-function accepts a string, takes its first character and looks it up within the ascii-charset; this position will be returned. The ```asc```-function is the opposite of the ```chr$```-function. There are valid uses for ```asc```, however, comparing strings (i.e. to bring them into alphabetical sequence) is *not* among them; in such many cases you might consider to compare strings directly with ```<```, ```=``` and ```>``` (rather than converting a string to a number and comparing this number).

## Example

```basic
input "Please enter a letter between 'a' and 'y': " a$
if (a$<"a" or a$>"y") print a$," is not in the proper range":end
print "The letter after ",a$," is ",chr$(asc(a$)+1)
```

## See also
 * [chr$](chr.html)
