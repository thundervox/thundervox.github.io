# end

Terminate your program.

## Synopsis

```basic
end
```

## Description

Terminate your program. Much (but not exactly) like the [```exit```](exit.html) command.

Note, that end may not end your program immediately; if you have opened a window or called [```clear screen```](clear-screen.html), yabasic assumes, that your user wants to study the output of your program after it has ended; therefore it issues the line ```---Program done, press RETURN---``` and waits for a key to be pressed. If you do not like this behaviour, consider using [```exit```](exit.html).

## Example

```basic
print "Do you want to continue ?"
input "Please answer y(es) or n(o): " a$
if (lower$(left$(a$,1))="n") then
  print "bye"
  end
fi
```

## See also

 * [exit](exit.html)
