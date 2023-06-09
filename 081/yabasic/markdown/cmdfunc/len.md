# len()

Return the length of a string.

## Synopsis

```basic
x=len(a$)
```

##  Description

The ```len```-function returns the length of its single string argument.

## Example

```basic
input "Please enter a password: " a$
if (len(a$)<6) error "Password too short !"
```

This example checks the length of the password, that the user has entered.

## See also

* [left$](left.html)
* [right$](right.html)
* [mid$](mid.html)
