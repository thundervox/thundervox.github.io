# chr$()

Accepts a number and returns the character at this position within the ASCII charset.

## Synopsis

```basic
character$=chr$(ascii)
```

## Description

The ```chr$```-function is the opposite of the [```asc```](asc.html)-function. It looks up and returns the character at the given position within the ascii-charset. It's typical use is to construct nonprintable characters which do not occur on your keyboard.

Nevertheless you won't use ```chr$``` as often as you might think, because the most important nonprintable characters can be constructed using [*escape-sequences*](escape-sequences.html) using the ```\```-character (e.g. you might use ```\n\``` instead of ```chr$(10)``` wherever you want to use the newline-character).

## Example

```basic
print "a",chr$(10),"b"
```

This will print the letters 'a' and 'b' in different lines because of the intervening newline-character, which is returned by ```chr$(10)```.

## See also

 * [asc](asc.html)
