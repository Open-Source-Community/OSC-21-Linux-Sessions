# Intel vs AT&T

## Syntax
### Intel

> **Instruction** <***dist***>, <***src***>  

### AT&T
> **Instruction** <***src***>, <***dist***>  

1. Comments
    * Intel
    > "    
    * AT&T
    > //
2. Regesters
    * Intel
    > eax
    * AT&I
    > %eax
3. Immediates
    * Intel
    > 0x47
    * AT&T
    > $0x47
4. Instructions
    * Intel
    > mov
    * AT&T
    > movb 
5. Indirect
    * Intel
    > [eax]
    * AT&T
    > (%eax)
6. Genral Indirect
    * Intel
    > [base + index*scale + disp]
    * AT&T
    > disp(base, index, scale)

## GCC (GNU Compiler Collection)

```sh
$ gcc <src_file> -o <bin(output)_file> # for compication
```

```sh
$ gcc -ggdb <src_file> -o <bin(output)_file> # produce debugging info for gdb 
```

## objdump
displays information about objet files created by 

```sh
$ gcc -c <src_file> -o <object_file>
```
these files can also be linked together forming elf executable
### Disassebling the executable

```sh
$ objdump -d <executable_file> # AT&T Syntax
```

```sh
$ objdump -d -M intel <executable_file> # Intel Syntax 
```

## hexdump
displays file content in hex, bin, dec, oct, or ascii format

```sh
dexdump -C <file> # see hexdump(1) man page
```

## xxd
makes hexdump or reverse

```sh
xxd <input_file> -o <output_file>.dump # for hexdump
```

```sh
xxd -r <input_file>.dump > <output_file> # for reverse
```

## GDB (GNU Debugger)

```sh
gdb <executable_file> # launches the debugger 
```

### GDB Commands

* ```help``` (***list available commands with its purpose***)
* ```run```  (***run the program passed to gdb***)
* ```run <argv>``` (***pass arguments to the program***)
* ```display[\FMT] <exp>``` (***Print value of expression EXP each time the program stops[stepping through instructions]***)
* ```undisplay <num>``` (***remove the statements tracked by display command***)
* ```x/FMT <address>``` (***examine memmory address (dereference first)***)
* ```print/FMT <exp>``` (***print the value of an expresion (no dereference)***)

### GDB Debugging Commands

* ```break``` (***set break point by address or debugging symbols***)
* ```delete <num>``` (***delete a break point***)
* ```info breakpoints``` (***display current tracked breackpoints***)
* ```step/stepi``` (***step one source line or one instruction line (steps into subroutines)***)
* ```until``` (***steps over subroutines***)
* ```continue``` (***continues until next breakpoint***)


### GDB Misc
* ```backtrace``` (***display a trace of the call stack (Good for troubleshooting SIG Faults) ***)
* ```set disassembly-flavor intel``` (***tell gdb to prefere intel syntax over at&t syntax***)

### GDB Command File
* ```gdb <executable> --command=<file>``` (***load startup commands to gdb from a file***)







