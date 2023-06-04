## Escape-sequences

*Escape-sequences* are the preferred way of specifying **special** characters. They are introduced by the ```\```-character and followed by one of a few regular letters, e.g. ```\n``` or ```\r``` (see the table below).

Escape-sequences may occur within any string at any position; they are replaced at parsetime (opposed to runtime), i.e. as soon as yabasic discovers the string, with their corresponding special character. As a consequence of this ```len("\a")``` returns 1, because yabasic replaces ```"\a"``` with the matching special character just before the program executes.

**Table 6.1. Escape sequences**

| Escape Sequence | Matching special character     |
| --------------- | ------------------------------ |
| \n              | *newline*                      |
| \t              | *tabulator*                    |
| \v              | *vertical tabulator*           |
| \b              | *backspace*                    |
| \r              | *carriage return*              |
| \f              | *formfeed*                     |
| \a              | *alert* (i.e. a beeping sound) |
| \\\             | *backslash*                    |
| \\'             | *single quote*                |
| \\"             | *double quote*                |
| \\xHEX          | *```chr$(HEX)```* (see below)                |

Note, that an escape sequences of the form \xHEX allows one to encode arbitrary characters as long as you know their position (as a hex-number) within the ascii-charset: For example ```\x012``` is transformed into the character ```chr$(18)``` (or ```chr$(dec("12",16))```. Note that \x requires a hexa-decimal number (and the hexadecimal string "12" corresponds to the decimal number 18).
