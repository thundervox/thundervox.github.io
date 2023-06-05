## Subroutines: Collecting your code for reuse in one program

### Purpose

Nobody wants to repeat oneself and therefore yabasic allows to collect arbitrary code, into subroutines, so that you may call it from multiple locations within you program. To this end, two conditions must be fulfilled:

1\. The subroutine neeeds to know details about what to do; that's why subroutines have parameters. E.g. in the overly simple subroutine ```sub add(a,b)``` (see the example below) the parameters would be a and b, specifying, which numbers to add.

*Remark: In certain cases a subroutine may want to find out, how many parameters it has been called with, by querying the special vairable [**```numparams```**]()<sup>**?**</sup>*.

2\. The subroutine needs to run without messing up the state of the program, at the point where it has been called. That's why many subroutines use [**local**]()<sup>**?**</sup> variables, which are different and isolated from all other variables in your program, even if they happen to have the same name. parameters (as described above) are, in addition to their primary function, also local variables.

*Remark: If a subroutine wants to remember some information between invocations, it may declare some of its variables as [**```static```**]()<sup>**?**</sup> instead of [**```local```**]()<sup>**?**</sup> function*.

To see these concepts explained in more detail (complete with examples), follow the links at the end of this section.

*Remark: You may notice, that other programming language may use other terms than subroutine for the same concept: ```function``` or ```procedure``` have been popular for pieces of code, that either return a value or not, and in other languages ```def``` is used to name both. And the term ```method``` is used in object-oriented languages. However yabasic is not object oriented, and regardless, if a piece of code produces a value or not, it can be encapsulated in a subroutine, so yabasic uses the function sub throughout*.

### A simple example

The short program below does nothing more than to add two numbers; for this purpose, it even defines a subroutine. This admittedly is more overhead, than you would normally take.

```basic
print "About to add two numbers."
input "Please enter first number: " x
input "Please enter second number: " y
print "Their sum is: ", add(x,y)

sub add(a,b)
  return a+b
end sub
```

If you run it, you would see:

```
About to add two numbers.
Please enter first number: 2
Please enter second number: 3
Their sum is: 5
```

Again, see the link at the end of this section for more explanations and examples (e.g. on ```local``` or ```static```, which have only been mentioned but not shown at work so far).

### See also

[**All commands for subroutines**]()<sup>**?**</sup>, where you will find links to the individual keywords related.
