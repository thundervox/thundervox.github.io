# max()

Return the larger of its two arguments.

## Synopsis

```basic
print max(a,b)
```

## Description

Return the *maximum* of its two arguments.

## Example

```
dim m(10)
for a=1 to 1000
  m=0
  For b=1 to 10
    m=max(m,ran(10))
  next b
  m(m)=m(m)+1
next a

for a=1 to 9
  print a,": ",m(a)
next a
```

Within the inner [```for```](for.html)-loop (the one with the loop-variable ```b```), the example computes the maximum of 10 random numbers. The outer loop (with the loop variable ```a```) now repeats this process 1000 times and counts, how often each maximum appears. The last loop finally reports the result.

Now, the interesting question would be, which will be approached, when we increase the number of iterations from thousand to infinity. Well, maybe someone could just tell me :-)

## See also

 * [min](min.html)
