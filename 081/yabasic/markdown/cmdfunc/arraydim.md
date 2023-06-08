# arraydim()

Returns the dimension of the array, which is passed as an array reference.

## Synopsis

```basic
a=arraydim(b())
```

## Description

If you apply the ```arraydim()```-function on a one-dimensional array (i.e. a vector) it will return ```1```, on a two-dimensional array (i.e. a matrix) it will return ```2```, and so on.

This is mostly used within subroutines, which expect an array among their parameters. Such subroutines tend to use the [```arraydim```](arraydim.html)-function to check, if the array which has been passed, has the right dimension. E.g. a subroutine to multiply two matrices may want to check, if it really is invoked with two 2-dimensional arrays.

## Example

```basic
dim a(10,10),b(10)
print arraydim(a()),arraydim(b())
```

This will print ```2 1```, which are the dimension of the arrays ```a()``` and ```b()```. You may check out the function [```arraysize```](arraysize.html) for a full example.

## See also

 * [arraysize](arraysize.html)
 * [dim](dim.html)
