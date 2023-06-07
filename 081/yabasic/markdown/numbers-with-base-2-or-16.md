## Numbers with base 2 or 16

In addition to the usual decimal notation (e.g. ```1234```), yabasic also supports numeric literals with base 2 or 16; examples are ```0b10011``` (the number 19, written with base 2) or ```0x34AF``` (the number 13487, written with base 16) respectively. Please note that these numbers (apart from the way you write them into your program) are no different from “ordinary” numbers and can be used in any place, where a normal number with base 10 would fit. E.g. you may compute the sine ```sin(0b110)```; so the base 2 (or 16) is just a different way of *representation*.

See <span class="notranslate">[**bin$**]()<sup>**?**</sup></span>, <span class="notranslate">[hex$](./cmdfunc/hex.html)</span> or <span class="notranslate">[**dec**]()<sup>**?**</sup></span> for related functions.
