## Specifying Filenames under Windows

As you probably know, windows uses the character ```\``` to separate the directories within a pathname; an example would be C:\yabasic\yabasic.exe (the usual location of the yabasic executable). However, the very same character ```\``` is used to construct [**escape sequences**]()<sup>**?**</sup>, not only in yabasic but in most other programming languages.

Therefore the string **C:\t.dat** does not specify the file t.dat within the directory C:; this is because the sequence ```\t``` is translated into the tab-character. To specify this filename, you need to use the string **C:\\t.dat** (note the double slash ```\\```).
