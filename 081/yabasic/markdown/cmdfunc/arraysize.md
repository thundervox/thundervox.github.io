# arraysize()

Returns the size of a dimension of an array.

## Synopsis

```basic
x=arraysize(a(),b)
```

## Description

The ```arraysize```-function computes the size of the specified dimension of a given array. Here, *size* stands for the maximum number, that may be used as an index for this array. The first argument to this function must be an [reference to an array](reference-on-arrays.html), the second one specifies, which of the multiple dimensions of the array should be taken to calculate the size. Please note, that ```arraysize``` returns the value that has been used in the actual ```dim```-statement, the real (internal) size of the array is allocated one larger in each dimension to have a first element at index 0; however this is not reflected by the output of ```arraysize```.

An Example involving subroutines: Let's say, an array has been declared as ```dim a(10,20)``` (that is a two-dimensional array or a matrix). If this array is passed as an [array reference](reference-on-arrays.html) to a subroutine, this sub will not know, what sort of array has been passed. With the ```arraydim```-function the sub will be able to find the dimension of the array, with the ```arraysize```-function it will be able to find out the size of this array in its two dimensions, which will be 10 and 20 respectively.

Our sample array is two dimensional; if you envision it as a matrix this matrix has 10 lines and 20 columns (see the ```dim```-statement above. To state it more formally: The first dimension (lines) has a size of 10, the second dimension (columns) has a size of 20; these numbers are those returned by ```arraysize(a(),1)``` and ```arraysize(a(),2)``` respectively. Refer to the example below for a typical usage.

## Example

```basic
rem
rem  This program adds two matrices elementwise.
rem

dim a(10,20),b(10,20),c(10,20)

rem  initialization of the arrays a() and b() 
for y=1 to 10:for x=1 to 20
   a(y,x)=int(ran(4)):b(y,x)=int(ran(4))
next x:next y

matadd(a(),b(),c())

print "Result:"
for x=1 to 20
   for y=10 to 1 step -1
      print c(y,x)," ";
   next y
   print
next x

sub matadd(m1(),m2(),r())

   rem  This sub will add the matrices m1() and m2()
   rem  elementwise and store the result within r()
   rem  This is not very useful but easy to implement.
   rem  However, this sub excels in checking its arguments
   rem  with arraydim() and arraysize()

   local x:local y

   if (arraydim(m1())<>2 or arraydim(m2())<>2 or arraydim(r())<>2) then
      error "Need two dimensional arrays as input"
   endif

   y=arraysize(m1(),1):x=arraysize(m1(),2)
   if (arraysize(m2(),1)<>y or arraysize(m2(),2)<>x) then
      error "The two matrices cannot be added elementwise"
   endif

   if (arraysize(r(),1)<>y or arraysize(r(),2)<>x) then
      error "The result cannot be stored in the third argument"
   endif

   local xx:local yy
   for xx=1 to x
      for yy=1 to y
         r(yy,xx)=m1(yy,xx)+m2(yy,xx)
      next yy
   next xx
 end sub
```

## See also

 * [arraydim](arraydim.html)
 * [dim](dim.html)
