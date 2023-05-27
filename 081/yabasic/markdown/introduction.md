# Chapter 1. Introduction

* [About this document](#about-this-document)
* [About yabasic](#about-yabasic)

## About this document

This document describes yabasic. You will find information about the yabasic interpreter (the program **yabasic** under Unix or **yabasic.exe** under Windows) as well as the language (which is, of course, a sort of basic) itself.

This document applies to version **2.90** of yabasic

However, it does *not* contain the latest news about yabasic or a FAQ. As such information tends to change rapidly, it is presented online only at www.yabasic.de.

Although basic has its reputation as a language for beginning programmers, this is not an introduction to programming at large. Rather this text assumes, that the reader has some (moderate) experience with writing and starting computer programs.

## About yabasic

yabasic is a traditional basic interpreter. It understands most of the typical basic-constructs, like ```goto```, ```gosub```, line numbers, ```read```, ```data``` or string-variables with a trailing ```'$'```. But on the other hand, yabasic implements some more advanced programming-constructs like subroutines or libraries (but *not* objects). yabasic works much the same under Unix and Windows.

yabasic puts emphasis on giving results quickly and easily; therefore simple commands are provided to open a graphic window, print the graphics or control the console screen and get keyboard or mouse information. The example below opens a window, draws a circle and prints the graphic:

```basic
open window 100,100
open printer
circle 50,50,40
text 10,50,"Press any key to get a printout"
clear screen
inkey$
close printer
close window
```

This example has fewer lines, than it would have in many other programming languages. In the end however yabasic lacks behind more advanced and modern programming languages like C++ or Java. But as far as it goes it tends to give you results more quickly and easily.
