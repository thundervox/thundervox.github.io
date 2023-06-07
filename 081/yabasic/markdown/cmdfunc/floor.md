# floor()

Compute the floor for its (float) argument.

## Synopsis

```basic
print floor(x)
```

## Description

The ```floor```-function returns the largest integer number, that is smaller or equal than its argument. For positive numbers ```x```, ```floor(x)``` is the same as ```int(x)```; for negaive numbers it can be different (see the example below).

## Example

```basic
print int(-1.5),floor(-1.5)
print int(-1),floor(-1)
print int(1.5),floor(1.5)
```

This example compares the functions ```int``` and ```floor```, starting with ```-1 -2```, then ```-1 -1``` and ending with ```1 1```, which shows the different behaviour of both functions.

## See also

 * [ceil](ceil)
 * [int](int.html)
 * [frac](frac.html)
 * [round](round.html)
