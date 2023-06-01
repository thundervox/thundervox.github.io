## Conditions and expressions

Well, bottomline there is no difference or distinction between *conditions* and *expressions*, at least as yabasic is concerned. So you may assign the result of comparisons to variables or use an arithmetic expression or a simple variable within a condition (e.g. within an ```if```-statement). So the constructs shown in the example below are all totally valid:

```basic
input "Please enter a number between 1 and 10: " a
rem   Assigning the result of a comparison to a variable
okay=a>=1 and a<=10
rem   Use a variable within an if-statement
if (not okay) error "Wrong, wrong !"
```

So conditions and expressions are really the same thing (at least as long as yabasic is concerned). Therefore the terms *conditions* and *expression* can really be used interchangeably, at least in theory. In reality the term *condition* is used in connection with ```if``` or ```while``` whereas the term *expression* tends to be used more often within arithmetic context.
