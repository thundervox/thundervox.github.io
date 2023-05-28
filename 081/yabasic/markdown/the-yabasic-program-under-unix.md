# Chapter 3. The yabasic-program under Unix

* [Starting yabasic](#starting-yabasic)
* [Options](#options)
* [Setting defaults](#setting-defaults)

## Starting yabasic

If your system administrator (vulgo *root*) has installed yabasic correctly, there are three ways to start it:

1. You may use your favorite editor (emacs, vi?) to put your program into a file (e.g. ```foo```). Make sure that the very first line starts with the characters ```'#!'``` followed by the full pathname of yabasic (e.g. ```'#!/usr/local/bin/yabasic'```). This she-bang-line ensures, that your Unix will invoke yabasic to execute your program (see also the entry for the [hash]()<sup>**?**</sup>-character). Moreover, you will need to change the permissions of your yabasic-program ```foo```, e.g. ```chmod u+x foo```. After that you may invoke yabasic to invoke your program by simply typing ```foo``` (without even mentioning yabasic). However, if your ```PATH```-variable does not contain a single dot ('.') you will have to type the full pathname of your program: e.g. ```/home/ihm/foo``` (or at least ```./foo```).
2. Save your program into a file (e.g. ```foo```) and type ```yabasic foo```. This assumes, that the directory, where yabasic resides, is contained within your ```PATH```-variable.
3. Finally your may simply type **yabasic** (maybe it will be necessary to include its full pathname). This will make yabasic come up and you will be asked to type in your program. Once you are finished, you need to type ```return``` twice, and yabasic will parse and execute your program.

### Note

This is not the preferred way of starting yabasic! Simply because the program, that you have typed, can not be saved and will be lost inevitably! There is no such thing as a save-command and therefore no way to conserve the program, that you have typed. This mode is only intended for quick hacks, and short programs, i.e. for using yabasic as some sort of fancy desktop calculator.

## Options

yabasic accepts a number of options on the command line.

See [chapter on options]()<sup>**?**</sup> for a complete list of all options, either on Unix or Windows.

## Setting defaults

If you want to set some options *once for all*, you may put them into your X-Windows resource file. This is usually the file ```.Xresources``` or some such within your home directory (type **man X** for details).

Here is a sample section, which may appear within this file:

```
yabasic*foreground: blue
yabasic*background: gold
yabasic*geometry: +10+10
yabasic*font: 9x15
```

This will set the foreground color of the graphic-window to *blue* and the background color to *gold*. The window will appear at position *10,10* and the text font will be *9x15*.
　
