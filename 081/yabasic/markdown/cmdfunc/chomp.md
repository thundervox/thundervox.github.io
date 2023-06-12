# chomp$()

Remove a single trailing newline from its string-argument; if the string does not end in a newline, the string is returned unchanged

## Synopsis

```basic
print chomp$("Hello !\n")
```

## Description

The ```chomp$```-function checks, if its string-argument ends in a newline and removes it eventually; for this purpose chomp$ can replace an [```if```](if.html)-statement. This can be especially useful, when you deal with input from external sources like [```system$```](system2.html).

You may apply ```chomp$``` freely, as it only acts, if there is a newline to remove; note however, that user-input, that comes from the normal input-statement, does not need such a treatment, because it already comes without a newline.

## Example

The following yabasic-program uses the unix-command **whoami** to get the username of the current user in order to greet him personally. This is done twice: First with the chomp$-function and then again with with an equivalent [```if```](if.html)-statement:

```basic
print "Hello " + chomp$(system$("whoami")) + " !"
user$ = system$("whoami")
if (right$(user$,1)="\n") user$=left$(user$,len(user$)-1)
print "Hello again " + user$ + " !"
```

## See also

 * [system$](system2.html)

