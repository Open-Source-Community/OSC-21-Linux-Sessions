# Linux Tools & Analysis

## Inter vs. AT&T Syntax

- Intel : (Windows)
- AT&T : (GNU/Linux)

| P.O.C | Intel | AT&T |
| --- | --- | --- |
| Assigning | Destination <- Source <br> `mov ebp, esp ; ebp = esp` | Source -> Destination <br> `mov %esp, %ebp ; esp + 0 = ebp` <br> registers get % and immediates get $|
| r/m32 values| [base + index*scale + disp] <br> `call DWORD PTR [ebx + esi*4 -0xe8]` | disp(base, index, scale) <br> `call *-0xe8(%ebx, %esi, 4)` |
| instruction on different sizes | movb (byte) <br> mov/movw (word) <br> movl (long) | mov dword ptr [eax] |

## gcc (GNU C Compiler)
- `gcc -o <output filename> <input file name>`
  - `bash gcc -o hello hello.c`
  - default output name if -o isn't specified is "a.out"
- Use -ggdb to make debug symbols
  - `gcc -ggdb -o <filename> <filename.c>`

## objdump - display information from object files
- Where "object file" can be an intermediate file created during compilation but before linking, or fully linked excutable (ELF file)
- the -d to disassemble a
file
- Can override the output syntax with “-M intel”
- `objdump -d -M intel hello`

## hexdump & xxd
- hexdump -C "for canonical" hex & ASCII view
- xxd - mkae a hexdump or reverse
  - `xxd hello > hello.dump`
  - `xxd -r hello.dump > hello`

## gdb - GNU debugger

A command line debugger

to start gdb : `gdb <program name> -x <command file>`

command file is a plain text file with a list of commnands the gdb should excute upon starting up (scripting)

### Commands
- `help` - internal navigation of available commands
- `run` or `r` - run the program
- `r <argv>` - run passing arguments
- `display` - prints statement every time the debugger stops
- `display/FMT EXP` - FMT can be:
  - `i` - display as asm instruction
  - `x` or `d` - display as hex or decimal
  - `b` or `h` or `w` - display as byte, halfword, word
  - `s` - character string, keep reading till null character
  - `<number>` - display number worth of things (instructions, bytes, words, strings, etc..)
- `info display` - see all outstanding display statements and their numbers
- `undisplay <num>` - remove display statement by num
- `x/FMT EXP` - examine memory at expression
- `print/FMT EXP` - print the value of an expression
- `break <address>` or `b` - set a breakpoint
- `info breakpoints` or `info b` - show currently set breakpoints
- `delete <num>` - delete breakpoint number num, where num came from `info b`
- `reverse-step` or `rs` - step program backward until it reaches the beginning of a previous source line
- `reverse-stepi` - step backward exactly one instruction
- `reverse-continue` or `rc` - continue program being debugged but run it in reverse
- `reverse-finish` - excute backward until just before the selected stack frame is called
- `reverse-next` or `rn` - step program backward, proceeding through subroutine calls
- `reverse-nexti` or `rni` - step backward one instruction, but proceed through called subroutines
- `set exec-direction (forward/reverse)` - set direction of excution
- `disassemble /r/m` - print instructions, r for raw, m for mixed
- `stepi` or `si` - steps one asm instruction at a time
- `step` or `s` - steps one source line at a time (if no source is available, works like stepi)
- `until` or `u` - steps until the next source line, not stepping into subroutines
- `set disassembly-flavor intel` - use intel syntax rather than AT&T
- `continue` or `c` - run until breakpoint
- `backtrace` or `bt` - print a trace of the call stack, showing all the functions which were called before the current function