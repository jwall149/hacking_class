#Introduction to Memory Hacking

###Goal

To alter values in a game, like lives, bullet, gold...
To pursue this, we must first find the values.

###Variables

Variables store the value, changed by the application used it. It can be one of our search target.

Variables have some notable properties:

- Memory Address (where the variable is located in memory, usually represented in hexadecimal notation with a leading 0x)
- Value (eg: 5)
- Data Type (the type of variable, eg: an integer, a string or a fractional number)
- Size (the number of bytes the variable takes up in memory; this can be tied to its data type)

###Search and Narrowing

To find the variable contains value we want to alter in the game, we should search and narrowing until we find it.

Ex: We want to alter number of coins (in game currency)

####First Search

In the game, we found 50 coins. we first search with 50 as the value and got a whole bunch of variables as the first search.

####Narrowing Searches

In the game, we got 5 more coins, total of 55, so the variable that store coins in game should change to 55. We search all variables last time we found to find one with 55. If we are lucky we can find it right away. If we are not we repeat the narrowing process until we found one.

##Data Type Choice

In computer programing, values are stored in type. And all these following type are call primitive type, support by all Operating System.

* Integers
  * 8 bit
  * 16 bit
  * 32 bit
  * 64 bit
* Floating Point
  * Float (4 bytes)
  * Double (8 bytes)
* Strings
  * 8 bit (ASCII)
  * 16 bit
* Pointers

Numbers like -5, 0, 2, 3, 100 represent integers, numbers like 1.43, 0.04, 1000.34 represent floating-points, and text like "Player Name:", "Lives" represent strings. These are the most common kinds of types to search for.

As for size: a 32-bit integer can vary from 2<sup>32</sup> different values, whereas an 8-bit integer can vary from 2<sup>8</sup> different values. Thus, a variable whose size is bigger can hold more possible values, but consumes more space in memory.

### Signed vs Unsigned Integers

For integers, there are two modes available. Signed integers can represent negative and positive numbers while unsigned integers can represent only non-negative values. For example, a 16-bit integer holds 2^16 possible values; this can vary from -32768 to 32767 if signed, or from 0 to 65535 if unsigned.

### Pointers

Pointers are memory addresses. Often times in programs, there are pointer variables which are simply variables whose value is a memory address to another variable in the program.

Variables can be edited in an advanced manner by going to Variable -> Edit Variable Address. An expression such as [0x1BE28] will be substituted with the pointer value read from 0x1BE28. This is also flexible allowing nesting and mathematical expressions such as [[0x1BE28] + 0x8] - 0x4].

### Endianness

Byte order, or endianness, determines how bytes are ordered to represent a value for a data type. The different types of endianness are big and little. Endianness affects all data types except for 8-bit integers, 8-bit strings, and byte arrays since with these data is grouped by single bytes.

For example, a 32-bit integer with a value of 1 is represented as the byte array 01 00 00 00 in little endian. The value of 1 is represented as the byte array 00 00 00 01 in big endian.

A tidbit about little endian is that integers of larger size can be represented in memory with the same layout as integers of smaller size, as long as the value is small enough to fit both sizes. For example, if you have a byte array in memory that is 01 00 00 00:

the first byte 01 could represent a 8-bit integer value of 1
the first two bytes 01 00 could represent a 16-bit integer value of 1
and all four bytes could represent 32-bit integer value of 1
Therefore one can search for a 8-bit integer as long as the value fits inside a 8-bit range, and could retrieve results even if the data type of the desired variable is actually of bigger size. Note the converse is not true for little endian: one can't search for a 32-bit integer and expect to find the value if it's really represented as an 8-bit integer in memory.

Fortunately, Intel processors, which is what Macs are based on nowadays, prefer little endian, which is what will be most commonly seen.
