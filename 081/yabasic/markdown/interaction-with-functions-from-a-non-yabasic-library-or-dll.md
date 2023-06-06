## Interaction with functions from a non-yabasic library or dll

**Note**

Under Unix, depending on the way yabasic has been built, this feature might have been disabled; the error message in this case will read like this build of yabasic does not support calling foreign libraries. To resolve this issue, you are invited to contact the maintainer.

**Note**

This is interesting, but somewhat advanced stuff. You will need a good understanding of various concepts of the C-language, especially pointers and structures as well as allocating and freeing blocks of memory. Please be aware, that mistakes or errors during calls to foreign functions or buffers may easily crash yabasic.

Yabasic allows to employ functionality from an external library; i.e. from a library, which is not written in yabasic, but rather in C; such a library is called a foreign library, as opposed to a library written in yabasic itself. Calling out to a foreign library can be useful, if such a library provides functionality, that can not be replicated in yabasic itself and for which a commandline-interface (which could be used via system) does not exist or is too cumbersome or slow. Examples would be libraries libVLC or libcurl which offer the functionality of vlc or curl to other programs, especially programs written in yabasic.

The foreign function interface of yabasic relies on the great libffi-library, a library making it easy to call other libraries dynamicaaly and the established standard for this task.

### Some Background

**Libraries**

Libraries (e.g. libcurl) are meant to provide functionality to other programs (here: yabasic and your yabasic-program). Libraries and programs must be linked together; this can happen either statically at compile-time or dynamically during the excution of the program. For yabasic as the program, static linking happens at the time, yabasic itself is build, whereas dynamic linking happen during the execution and under control of your yabasic-program. So the foreign function interface deals with dynamic (or runtime) linking to external libraries. This linking is done by yabasic behind the scene, when you invoke foreign_function_call; this function, after loading the library, directly calls the specified function therein.

Which functions are available differs from library to library and you should already have this information before you try the library with yabasic.

**Types**

If you want to use a function from a foreign library, you will need to deal with the fact, that each function requires several parameters and returns exactly one. These parameters have a wide variety of types which need to be mapped to the two types (numbers and strings) known by yabasic. Here are the types available for foreign functions, grouped by the way, they are handled in yabasic:

```uint8,int8,uint16,int16,uint32,int32,uint64,int64,float,double,char,short,int,long```

In C all these types are used to represent numbers (integer or floating point) with various degrees of precision. When invoking foreign_function_call you need to pass strings, which specify the right type as well as the actual yabasic-value, which will then be converted accordingly. Which types a foreign function expects can be looked up e.g. from its manpage.

```string```

Strings for foreign functions directly map to strings of yabasic. So if you specify this type for a parameter of a foreign function, the matching value is simply a yabasic string. If you specify string as the return value of a foreign function you should use the variant of calling it, which returns a string, i.e. foreign_function_call$.

```buffer```

You should specify a buffer as the type of a parameter or the return type, if the foreign function expects a structure or a pointer to a memory area; see structures and buffers for details.

### Three simple examples

**Computing the cosine**

This first example prints the cosine of 2, not by using yabasics own cos-function but by calling out to the standard C-library:

```
if peek$("os")="windows" then
  lib$ = "msvcrt.dll"
else
  lib$ = "libm.so.6"
endif

print "cos(2): ",foreign_function_call(lib$,"double","cos","double",2)
```

The first lines determine the name of the library, which is different under Unix and Windows. The call to foreign_function_call than just states the name of the library, the return type ("double") of the function and then its name ("cos"), as well as type and value (2) of its argument. The final result -0.416147 then is the same as from the the internal cos-function, which is no surprise, because yabasic is already statically linked to the standard C-library and uses its function to compute the cosine.

**Searching a string within another string**

A second example:

```basic
if peek$("os")="windows" then
  lib$ = "msvcrt.dll"
else
  lib$ = "libm.so.6"
endif

print foreign_function_call$(lib$,"string","strstr","string","foobar","string","ob","options","copy_string_result")
```

This example calls the strstr-function from the standard C-library; this function accepts two string arguments and returns a string, which is the first (if any) appearance of the second string within the first one (remark: this function makes more sense in C than in yabasic). Please note the option "copy_string_result", which advices yabasic to return a copy of the result of strstr; otherwise your program might crash, because strstr simply returns a pointer to a part of its first argument, a string that will later be freed by yabasic.

**Showing a message box under Windows**

This example is windows only; it shows a standard Windows message box with the given title and message:

```basic
message_box("Hello World !","Message from yabasic")

sub message_box(message$, title$)
  msgptr$ = foreign_buffer_alloc$(len(message$)+1)
  foreign_buffer_set msgptr$, 0, message$
  titleptr$ = foreign_buffer_alloc$(len(title$)+1)
  foreign_buffer_set titleptr$, 0, title$
  hwnd$ = foreign_function_call$("user32.dll", "buffer", "GetActiveWindow")
  ret = foreign_function_call("user32.dll", "int32", "MessageBoxA", "buffer", hwnd$, "buffer", msgptr$, "buffer", titleptr$, "uint32", 0)
  foreign_buffer_free msgptr$
  foreign_buffer_free titleptr$
  return ret
end sub
```

The relevant Windows-function MessageBoxA is found within the library user32.dll; most of the example deals with properly allocating, handling and freeing buffers to hold the supplied text-snippets. Thanx to Jean-Marc Duro for this example.

### Internal steps during a call to a foreign function

A remark on libffi: this is the library which allows yabasic to call functions from other libraries libffi is used by many other programming-languages for the same purpose; in yabasic it is linked statically (rather than dynamically) so that its functionality is available right from the start. Summing up: libffi itself need not be loaded but helps to call functions from other loaded libraries.

Here is the sequence of events during a foreign function call (e.g. foreign_function_call):

* Yabasic parses the type specifications and argument values provided and collects the necessary information for libffi.

* The named library is loaded with the appropriate call (which is different under Windows and Unix). This step might easily fail, e.g. if you misspelled the name of the library or your system cannot find the library.

* With the help of libffi the named function is invoked.

* If you specified the option unload_library, the library that has been loaded is unloaded again.

* The return value of the function is converted to a form suitable for yabasic and your program continues.

Errors are reported during every step.

### Abbreviations for long names

Yabasics functions for dealing with foreign libraries start with foreign_function or foreign_buffer (e.g. foreign_buffer_alloc). To help in typing, these names can all be abbreviated by contracting foreign_function into frnfn and foreign_buffer into frnbf. In the examples below, both forms appear.

### Structurs and buffers

The C-language provides a wide variety of simple datatypes (like numbers an strings) and allows to aggregate simple datatypes to structures such a structure contains a set of simple types arranged without overlap (but sometimes with gaps). Yabasic on itself does not know the internals of a structure but rather treats it as a uniform buffer. Structure and buffer are just flipsides of the same memory area viewed either from C or yabasic. For your yabasic-program a buffer is represented by a handle, which is just a simple printable string (containing the size and the memory adress).

The detailed knowledge about the simple types within a structure must be coded into your program, which uses the command (or function) foreign_buffer_set and foreign_buffer_get. Both functions require type and offset (which needs to be looked up in documentation of the foreign library) of the simple type within the structure and a handle to the buffer, which contains the structure.

Beeing essentially a memory area, a buffer is created with foreign_buffer_alloc and destroyed with foreign_buffer_free if needed no more.

Besides representing a structure, a buffer can also provide room to store raw areas of memory for use by the foreign library; example might be image- or sound-content.

### Two more complex examples

**Dealing with time**

The example below deals with the time functions from the standard C-library; some of them deal with the tm structure for keeping the segmented time; to understand the example it is good to have the tm-structure at hand; see below. In addition it might be helpful to consult the manpages of the various C-functions (e.g. localtime)involved.

```c
struct tm {
    int tm_sec;    /* Seconds (0-60) */
    int tm_min;    /* Minutes (0-59) */
    int tm_hour;   /* Hours (0-23) */
    int tm_mday;   /* Day of the month (1-31) */
    int tm_mon;    /* Month (0-11) */
    int tm_year;   /* Year - 1900 */
    int tm_wday;   /* Day of the week (0-6, Sunday = 0) */
    int tm_yday;   /* Day in the year (0-365, 1 Jan = 0) */
    int tm_isdst;  /* Daylight saving time */
};
```

The example plays with the two forms of keeping the time, either as unix-time (number of seconds since epoch) or as a segmented time (sec, min, etc.). The six steps are each introduced by comments, please see below.

```basic
# First: Determine the correct library depending on OS
#
if peek$("os")="windows" then
  lib$ = "msvcrt.dll"
else
  lib$ = "libm.so.6"
endif

# Second: Get the unix-time
#
# time() has a pointer argument to store the result (in addition to returning it)
# we pass NULL, so only the return value is relevant
#
null$ = foreign_buffer_alloc$(-1)
now = foreign_function_call(lib$,"int","time","buffer",null$)
print "Seconds since the epoch: ",now

# Third: Convert the unix-time to a segmented time
#
# localtime() does not accept the time-value as an argument, but rather requires a pointer
# to the time-value, so we construct a buffer for one int and put in our value
now$ = foreign_buffer_alloc$(foreign_function_size("int"))
foreign_buffer_set now$,0,"int",now

# Dump the buffer for educational purpose
print "Dump of buffer:          ",foreign_buffer_dump$(now$)
# localtime() returns a structure with the componentes (year, day, sec, etc.) as elements
local$ = foreign_function_call$(lib$,"buffer","localtime","buffer",now$)

# Fourth: Get the current year from the resulting buffer
#
# assuming, that year is the sixth element of the structure
# so offset is 5
offset = 5 * foreign_function_size("int")
year = foreign_buffer_get(local$,offset,"int")
print "Current year:            ", year + 1900
# Fifth: manipulate the segmented time

#
# set year to something else
foreign_buffer_set local$,offset,"int",year-50

# Sixth: convert time-structure from localtime into ascii
#
print "50 years back:           ", foreign_function_call$(lib$,"string","asctime","buffer",local$)
```

On my computer this program produces the following output:

```
Seconds since the epoch: 1559014899
Dump of buffer:          F3ADEC5C
Current year:            2019
50 years back:           Tue May 28 05:41:39 1969
```

**Getting the version of libcurl**

This final example just invokes libcurl to report its version. This is somewhat involved, because the matching function curl_version_info (see its man-page) returns a structure, which contains a pointer to a string, as can be seen from the structures definition:

```
typedef struct {
  CURLversion age;          /* see description below */
  const char *version;      /* human readable string */
  unsigned int version_num; /* numeric representation */
  const char *host;         /* human readable string */
  int features;             /* bitmask, see below */
  char *ssl_version;        /* human readable string */
  long ssl_version_num;     /* not used, always zero */
  const char *libz_version; /* human readable string */
  const char * const *protocols; /* protocols */

  ...                       /* more lines omitted */

} curl_version_info_data;
```

Please note, that the yabasic-code below uses abbreviations (e.g. frnfn_call instead of foreign_function_call.

```
# Get structure with version info
info$ = frnfn_call$("libcurl.so.4","buffer","curl_version_info","int",1)
# dump it for reference
print frnbf_dump$(info$,32)
# assume, that the pointer to version string is at offset 8
sinfo$ = frnbf_get_buffer$(info$,8)
# print readable version
print frnbf_get$(sinfo$,0,10)
```

The printing of [**frnbf_dump**]()<sup>**?**</sup> gives a hint on the internal offsets within the structure and helps to determine that offset of 8 for the next call.

On my system this program produces ```7.61.1``` for the version of curl.

### See also

[**foreign_function_call**]()<sup>**?**</sup>, [**foreign_function_call2**]()<sup>**?**</sup>, [**foreign_function_size**]()<sup>**?**</sup>, [**foreign_buffer_alloc**]()<sup>**?**</sup>, [**foreign_buffer_free**]()<sup>**?**</sup>, [**foreign_buffer_size**]()<sup>**?**</sup>, [**foreign_buffer_dump**]()<sup>**?**</sup>, [**foreign_buffer_set**]()<sup>**?**</sup>, [**foreign_buffer_set_buffer**]()<sup>**?**</sup>, [**foreign_buffer_get**]()<sup>**?**</sup>, [**foreign_buffer_get2**]()<sup>**?**</sup>, [**foreign_buffer_get_buffer**]()<sup>**?**</sup>, [**system**]()<sup>**?**</sup>

