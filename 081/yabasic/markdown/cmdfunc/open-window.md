# open window

Open a graphic window.

## Synopsis

```basic
open window x,y
open window x,y,"font"
```

## Description

The ```open window```-command opens a window of the specified size. Only one window can be opened at any given moment of time.

An optional third argument specifies a font to be used for any text within the window. It can however be changed with any subsequent [```text```](text.html)-command.

## Example

```basic
for a=200 to 400 step 10
  open window a,a
  for b=0 to a
    line 0,b to a,b
    line b,0 to b,a
  sleep 0.1
  close window
next a
```

## See also

 * [close window](close-window.html)
 * [text](text.html)
