## Libraries: Collecting your code for reuse in many programs

### Purpose

*Libraries* build upon [**subroutines**]()<sup>**?**</sup> and take the concept of code-reuse one step further: They allow code to be shared between *different* programs (as compared to subroutines, which on their own allow code-reuse within a single program only). Moreover, it is possible and in fact common, that the author of a library and the author of a program using that library, are different persons, each writing their respective code on their own.

## A simple example

Here is a program, that asks the user for two numbers and then uses a library ```adder``` to add those:

```
import adder

print "About to add two numbers."
input "Please enter first number: " x
input "Please enter second number: " y
print "Their sum is: ", adder.add(x,y)
```

The statement ```import adder``` pulls in code from a very simple *library* ```adder.yab```:

```basic
sub add(a,b)
  return a+b
end sub
```

If you run it, you might see:

```
About to add two numbers.
Please enter first number: 3
Please enter second number: 4
Their sum is: 7
```

Compared with the very similar example for [**subroutines**]()<sup>**?**</sup>, there are two differences:

The code of the subroutine add has been moved to its own file ```adder.yab```.

1\. The subroutine add needs to be called as adder.add, which consists of filename (```adder.yab``` but without the ending ```.yab```) and the name of the subroutine (```add```) within that file.

2\. This is an exampe of *namespaces*.

### Namespaces

When the executable code is devided between a *main program file* and (multiple) *libraries* it is important to keep their subroutines and variables seperate. To this end yabasic internally prefixes the subroutines and variables defined in a library with the shortened name of the library. E.g. in the example above, the subroutine ```add``` from the library ```adder.yab``` is prefixed by this library-name and ends up as beeing defined as ```adder.add```.

Subroutines and variables defined within the main program are prefixed with ```main```; this prefix is fixed and not related to the actual filename of the main-program. Normally, however, there is no need to use this prefix explicitly; it only helps yabasic to keep everything apart.

### See also

[**import**]()<sup>**?**</sup>, [**export**]()<sup>**?**</sup>, [**subroutines**]()<sup>**?**</sup>
