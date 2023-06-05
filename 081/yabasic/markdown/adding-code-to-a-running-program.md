## Adding code to a running program

### Purpose

Normally, you write programs in yabasic and specify all the necessary logic and calculations within your program. Once you are done, you invoke it, probably multiple times; and while it is running, it does not change.

However, there are some commands within yabasic, that allow to blur the line between writing and execution. Namely [**eval**]()<sup>**?**</sup>, [**eval$**]()<sup>**?**</sup>, [**compile**]()<sup>**?**</sup>, [**execute**]()<sup>**?**</sup> and [**execute$**]()<sup>**?**</sup> allow to create and execute new yabasic-code while your program is running. This comes in handy, if the code to be used comes from the user of your program and will only be known after your program has started. A simple example is the yabasic-code to calculate the maximum of a user-supplied expression within a given range; find it as an example for [**eval**]()<sup>**?**</sup>. In the same way, one may write a program to plot an arithmetic function, whose definition is entered by the user.

Note: Even if the commands listed above allow to change the yabasic-program, that is currently running, the file where the program is stored, does not change. Therefore, the changes to the running program are not permanent.

### How the various functions and commands differ

The most simple functions are [**eval**]()<sup>**?**</sup> and [**eval$**]()<sup>**?**</sup>; they compile an expression (with a numeric or string result), e.g. and execute it right away. The compiled code is remembered, so that it need not be compiled again, when the sames expression is executed again; this caters efficiency. However these functions only accept a single expression and nothing else.

If you need more complex computation and logic, the process needs to be split: First create a new subroutine with the [**compile**]()<sup>**?**</sup>-command, then execute this subroutine (maybe multiple times) via [**execute**]()<sup>**?**</sup> or [**execute$**]()<sup>**?**</sup>. This allows to use the broad logic available in subroutines (e.g. conditions, loops, local variables or even other subroutines) and therefore much more complex calculations than with [**eval**]()<sup>**?**</sup>. If you want to use [**compile**]()<sup>**?**</sup> multiple times within your program (e.g. in a loop), you may want to enumerate the functions you create to avoid name-clashes (as shown in the examples of [**compile**]()<sup>**?**</sup>).

To invoke the subroutines created, you need to execute them with [**execute**]()<sup>**?**</sup> or [**execute$**]()<sup>**?**</sup>, which require the name of the function (a string) as their first argument.

