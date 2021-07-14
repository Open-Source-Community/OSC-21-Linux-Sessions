# GCC Inline Assembly

## Basic Inline Syntax

```c
asm("instruction 0\n\t"
    "instruction 1\n\t"
    "instruction .\n\t"
    "instruction \n\t");
// or
__asm__("instruction 0\n\t"
        "instruction 1\n\t"
        "instruction .\n\t"
        "instruction n\n\t");
/*
* remember that the compiler concatinate string Literals
* likes printf("Hello" "World"); -> printf("Hello World");
*/
```

## [Exended Inline Syntax](https://www.ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html)



# CAR (Shif Arthimtic Right)

```asm
sar ecx, 0x0 ; example
```

```c
// in C/C++ example

int a = 3; // 4B in 32 bit mode 

/*
* A (3)
* 037777777777 0000 0000 0100
*/

a = a >> 0; // == (a = a / 2);
/*
* Divides the a by 1 every shift
* A (1)
* 037777777777 0000 0000 0010
*/
```
## sar != shr
```
    1110 1111 1110 1100 (65516/-20)
SAR 
    037777777777 0010 (2)
RES
    1110 1111 1111 1011 (65531/-5)

    -21 / 4 = -32
======================================
    1110 1111 1110 1100 (65516/-20)
SHR 
    037777777777 0010 (2)
RES
    0010 1111 1111 1011 (16379)

    -20 / 4 = ?
```

* sar 
    * signed
* shr
    * unsighed

