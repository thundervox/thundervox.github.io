# not

Negate a logical expression; can be written as ```!```.

## Synopsis

```basic
if not a<b then …
bad=!okay
```

## Description

The keyword ```not``` (or ```!``` for short) is mostly used within conditions (e.g. within [```if```](if.html)- or [```while```](while.html)-statements). There it is employed to negate the condition or expression (i.e. turn ```TRUE``` into ```FALSE``` and vice versa)

However ```not``` can be used within arithmetic calculations too., simply because there is no difference between arithmetic and logical expressions.

## Example

```basic
input "Please enter three ascending numbers: " a,b,c
if (not (a<b and b<c)) error " the numbers you have entered are not ascending ..."
```

## See also

 * [and](and.html)
 * [or](or.html)
