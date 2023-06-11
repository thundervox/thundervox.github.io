# min()

Return the smaller of its two arguments.

## Synopsis

```basic
print min(a,b)
```

## Description

Return the *minimum* of its two argument.

## Example

```basic
dim m(10)
for a=1 to 1000
  m=min(ran(10),ran(10))
  m(m)=m(m)+1
next a

for a=1 to 9
  print a,": ",m(a)
next a
```

For each iteration of the loop, the lower of two random number is recorded. The result is printed at the end.

## See also

* [max](max.html)
