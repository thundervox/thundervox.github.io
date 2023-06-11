# new curve

Start a new curve, that will be drawn with the ```line```-command.

## Synopsis

```basic
new curve
line to x,y
```

## Description

The ```new curve```-function starts a new sequence of lines, that will be drawn by repeated ```line to```-commands.

## Example

```basic
open window 200,200
ellipse(100,50,30,60)
ellipse(150,100,60,30)
sub ellipse(x,y,xr,yr)
  new curve
  for a=0 to 2*pi step 0.2
    line to x+xr*cos(a),y+yr*sin(a)
  next a
  close curve
end sub
```

This example defines a subroutine ```ellipse``` that draws an ellipse. Within this subroutine, the ellipse is drawn as a sequence of lines started with the ```new curve``` command and closed with [```close curve```](close-curve.html).

## See also

 * [line](line.html)
 * [close curve](close-curve.html)
