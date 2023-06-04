## References on arrays

*References on arrays* are the only way to refer to an array *as a whole* and to pass it to subroutines or functions like [**arraydim**]()<sup>**?**</sup> or [**arraysize**]()<sup>**?**</sup>.

While (for example) ```a(2)``` designates the second element of the array a, ```a()``` (with empty braces) refers to the array ```a``` itself. ```a()``` is called an *array reference*. A nice example is the bultin function [**split**]()<sup>**?**</sup>, that accepts an array-reference and modifies the content of this array.

You may also pass to and use array reference within your own subroutines; these subroutines will then be able to modify the array you have passed in often this is intended.

Passing an array reference does not create a copy of the array; this has some interesting consequences:

* *Speed and space*: Creating a copy of an array would be a time and memory consuming operation; passing just a reference is cheap and fast.

* Returning many values: A subroutine, that wants to give back more than one value, may require an array reference among its arguments and then store its many return values within this array. This is the only way to return more than one value from a subroutine.

### An example

The following program creates two subroutines (```print_words``` and ```upcase_words```), that operate on an array of words (```words$()``` below):

```basic
dim words$(4)
for i=1 to 4
  read words$(i)
next i

print_words(words$())
upcase_words(words$())
print_words(words$())

sub print_words(w$())
  local i
  for i=1 to arraysize(w$(),1)
    print w$(i)," ";
  next i
  print    
end sub

sub upcase_words(w$())
  local i
  for i=1 to arraysize(w$(),1)
    w$(i) = upper$(w$(i))
  next i
end sub

data "case","does","not","matter"
```

If you run this program, you will get this output:

```
case does not matter
CASE DOES NOT MATTER
```

	    
