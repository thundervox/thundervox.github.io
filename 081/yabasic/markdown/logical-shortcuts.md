## Logical shortcuts

*Logical shortcuts* are no special language construct and there is no keyword for them; they are just a way to evaluate *logical expressions*. Logical expressions (i.e. a series of conditions or comparisons joined by [**and**]()<sup>**?**</sup> or [**or**]()<sup>**?**</sup>) are only evaluated until the final result of the expression can be determined. An example:

```basic
if (a<>0 and b/a>2) print "b is at least twice as big as a"
```

The logical expression ```a<>0 and b/a>2``` consists of two comparisons, both of which must be true, if the ```print``` statement should be executed. Now, if the first comparison (```a<>0```) is ```false```, the whole logical expression can never be ```true``` and the second comparison (```b/a>2```) need not be evaluated.

This is exactly, how yabasic behaves: The evaluation of a composed logical expressions is terminated immediately, as soon as the final result can be deduced from the already evaluated parts.

In practice, this has the following consequences:

* If two or more comparisons are joined with ```and``` and one comparison results in ```false```, the logical expression is evaluated no further and the overall result is ```false```.

* If two or more comparisons are joined with ```or``` and one comparison results in ```true```, the logical expression is evaluated no further and the result is ```true```.

“Nice, but whats this good for ?”, I hear you say. Well, just have another look at the example, especially the second comparison (```b/a>2```); dividing ```b``` by ```a``` is potentially hazardous: If a equals zero, the expression will cause an error and your program will terminate. To avoid this, the first part of the comparison (```a<>0```) checks, if the second one can be evaluated without risk. This pre-checking is the most common usage and primary motivation for *logical shortcuts* (and the reason why most programming languages implement them).
