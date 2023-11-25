## Memory

* Data in memory is stored in bytes, which are composed of bits.
* Bytes in memory can be used to reference other bytes, allowing for the storage of references to additional data.(pointer)
* The amount of memory available on a machine is limited, so it is valuable to minimize the amount of memory used by an algorithm.
* Accessing a byte or a fixed number of bytes (such as 4 bytes or 8 bytes for 32-bit and 64-bit integers) is considered a basic operation, roughly equivalent to a single unit of computational work.

1. Bit: A bit is the basic unit of information in computing, representing a state with either a 0 or 1.
2. Byte: A byte is a group of 8 bits. It can represent values from 0 to 255 in binary format.
3. Fixed-Width Integer: It is an integer represented by a fixed number of bits, such as 32 bits (4 Bytes) or 64 bits (8 Bytes). The number is stored in binary format, with each byte separated by spaces.

### Memory Example in a bounded canvas
|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|1Byte (8bits)|
|-|-|-|-|-|-|-|-|-|-|
|(No. 1)<br>|(No. 2)<br>|(No. 3)<br>No.7|(No. 4)<br>|(No. 5)<br>|(No. 6)<br>|(No. 7)<br>|(No. 8)<br>|(No. 9)<br>|(No. 10)<br>|
|(No.11)<br>|(No.12)<br>|(No.13)<br>|(No.14)<br>|(No.15)<br>|(No.16)<br>|(No.17)<br>|(No.18)<br>|(No.19)<br>|(No. 20)<br>|
|(No.21)<br>|(No.22)<br>|(No.23)<br>|(No.24)<br>0000 0011|(No.25)<br> **0** |(No.26)<br> **0** |(No.27)<br> **0** |(No.28)<br>|(No.29)<br>|(No. 30)<br>|
|(No.31)<br>|(No.32)<br>|(No.33)<br>|(No.34)<br>|(No.35)<br>|(No.36)<br>|(No.37)<br>|(No.38)<br>|(No.39)<br>|(No. 40)<br>|

We can use pointers to refer to a specific memory slot from another slot. For instance, if we want to store a value in slot No. 7, we can use a pointer in slot No. 3 to point to slot No. 7.

We can also store fixed-width numbers in the memory slots, such as the number 3 (0011 in binary) that is stored in slots No. 24 to No. 27, in little-endian format.

Finally, we can convert strings to ASCII codes and store them as bytes in memory slots. For example, the capital letter A is represented by the ASCII code 65, which can be stored as a byte in memory.
