# 1\. Basic Data Types and Structures

In addition to the standard data types available in C, the Goc preprocessor handles several other types specific to GEOS. These are all defined in the file **geos.h**. Some of these types, shown below, were carried over from the world of assembly language. 

<!-- ![GOCLanguage_1_simpleTypes.gif](GOCLanguage_1_simpleTypes.gif) -->

| Type Name | Description                                  |
| --------- | -------------------------------------------- |
| byte      | An unsigned, 8-bit field.                    |
| sbyte     | A signed, 8-bit field (same as char).        |
| word      | An unsigned, 16-bit field.                   |
| wchar     | An unsigned, 16-bit field (same as word).    |
| sword     | A signed, 16-bit field (same as short).      |
| dword     | An unsigned, 32-bit field.                   |
| sdword    | A signed, 32-bit field (same as long).       |
| Boolean   | A type (16 bits) used for Boolean functions. |

The Boolean type behaves as most Boolean types--any nonzero value represents a ``true`` state, and zero represents the ``false`` state. Throughout the documentation, ``true`` and ``false`` are taken to be these meanings. Note that the constants TRUE and FALSE are defined and may be used as return values from your functions and methods. Do not compare Boolean variables, however, against these constants. A Boolean may be ``true`` without actually equaling the TRUE value.

* [Records and Enumerated Types](GOCLanguage_2.md)
* [Handles and Pointers](GOCLanguage_3.md)
* [Fixed Point Structures](GOCLanguage_4.md)
