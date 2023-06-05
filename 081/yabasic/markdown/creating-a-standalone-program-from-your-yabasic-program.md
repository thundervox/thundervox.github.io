## Creating a *standalone* program from your yabasic-program

Sometimes you may want to give one of your yabasic-programs to other people. However, what if those other people do not have yabasic installed ? In that case you may create a standalone-program from your yabasic-program, i.e. an executable, that may be executed on its own, standalone, even (and especially !) on computers, that do not have yabasic installed. Having created a standalone program, you may pass it around like any other program (e.g. one written in C) and you can be sure that your program will execute right away.

Such a *standalone*-program is simply created by copying the full yabasic-interpreter and your yabasic-program (plus all the libraries that it may ```import```) together into a single, new program, whose name might be chosen at will (under windows of course it should have the ending ```.exe```). If you decide to create a standalone-program, there are three facilities in yabasic, that you may use:

* The [**```bind```**]()<sup>**?**</sup>-command, which does the actual job of creating the standalone program from the yabasic-interpreter and your program.

* The command-line Option --bind (see options), which does the same from the command-line.

* The special peek("isbound"), which may be used to check, if the yabasic-program containing this peek is bound to the interpreter as part of a standalone program.

With these bits you know enough to create a standalone-program. Actually there are two ways to do this: on the command line and from within your program.

### Creating a standalone-program from the command line

Let's say you have the following very simple program within the file foo.yab:

```basic
print "Hello World !"
```

Normally you would start this yabasic-program by typing yabasic foo.yab and as a result the string Hello World ! would appear on your screen. However, to create a standalone-program from foo.yab you would type:

```powershell

yabasic -bind foo.exe foo.yab

```

This command does not execute your program foo.yab but rather create a standalone-program foo.exe. Note: under Unix you would probably name the standalone program foo or such, omitting the windows-specific ending .exe.

Yabasic will confirm by printing something like: ```---Info: Successfully bound 'yabasic' and 'foo.yab' into 'foo.exe```.

After that you will find a program foo.exe (which must be made executable with the chmod-command under Unix first). Now, executing this program foo.exe (or foo under Unix) will produce the output Hello World !.

This newly created program foo.exe might be passed around to anyone, even if he does not have yabasic installed.

### Creating a standalone-program from within your program

It is possible to write a yabasic-program, that binds itself to the yabasic-interpreter. Here is an example:

```basic
if (!peek("isbound")) then
  bind "foo"
  print "Successfully created the standalone executable 'foo' !"
  exit
endif
print "Hello World !"
```

If you run this program (which may be saved in the file foo.yab) via yabasic foo.yab, the peek("isbound") in the first line will check, if the program is already part of a standalone-program. If not (i.e. if the yabasic-interpreter and the yabasic-program are separate files) the bind-command will create a standalone program foo containing both. As a result you would see the output Successfully created the standalone executable 'foo' !. Note: Under Windows you would probably choose the filename foo.exe.

Now, if you run this standalone executable foo (or foo.exe), the very same yabasic-program that is shown above will be executed again. However, this time the peek("isbound") will return TRUE and therefore the condition of the if-statement is false and the three lines after then are not executed. Rather the last print-statement will run, and you will see the output Hello World !.

That way a yabasic-program may turn itself into a standalone-program.

### Points to consider before creating a standalone program

* The new standalone program will be at least as big as the interpreter itself, which is typically a few hundred kilobytes.

* There is no easy way to extract your yabasic-program from within the standalone program: If you ever want to change it, you should keep it around as a separate file.

* If a new version of yabasic becomes available, you might want to recreate your standalone program to take advantage of bugfixes and improvements.

### See also

The bind-command, the peek-function and the command line options.
