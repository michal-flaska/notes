# Assembly Programming Guide

## How Computers Actually Work

Your CPU executes instructions in machine code (binary). Assembly is just human-readable machine code - nearly 1:1 mapping. When you write assembly, you're directly controlling the CPU.

Key Components:
- CPU/Processor: Executes instructions, does math, logic operations
- Registers: Super fast storage inside CPU (think variables that live in the processor)
- RAM/Memory: Slower storage outside CPU, holds your program and data
- Cache: Fast memory between CPU and RAM (L1, L2, L3)

How a Program Runs:
1. OS loads your program into RAM
2. CPU fetches instruction from memory
3. CPU decodes what to do
4. CPU executes it
5. Repeat until program ends

## Memory & Addressing

Memory is just a giant array of bytes. Each byte has an address (0x0, 0x1, 0x2...).

```
Address   | Data
----------|------
0x1000    | 0x42
0x1001    | 0xFF
0x1002    | 0x00
```

Sizes:
- Byte = 8 bits
- Word = 2 bytes (16 bits)
- Dword = 4 bytes (32 bits)
- Qword = 8 bytes (64 bits)

## x86-64 Registers (Most Common)

General Purpose (64-bit):
- `rax` - Accumulator (return values, math)
- `rbx` - Base (general use)
- `rcx` - Counter (loops)
- `rdx` - Data (general use)
- `rsi` - Source index (string ops)
- `rdi` - Destination index (string ops)
- `rbp` - Base pointer (stack frame)
- `rsp` - Stack pointer (top of stack)
- `r8`-`r15` - Extra registers

32-bit versions: `eax`, `ebx`, etc.
16-bit versions: `ax`, `bx`, etc.
8-bit versions: `al`, `bl`, etc.

Special:
- `rip` - Instruction pointer (current instruction address)
- `rflags` - Status flags (zero, carry, overflow, etc.)

## Basic Instructions

### Data Movement
```asm
mov rax, 5          ; rax = 5
mov rbx, rax        ; rbx = rax
mov [rax], rbx      ; Write rbx to memory at address in rax
mov rax, [rbx]      ; Read from memory at address in rbx into rax
lea rax, [rbx+8]    ; Load address (rax = rbx + 8, but don't access memory)
```

### Arithmetic
```asm
add rax, 5          ; rax += 5
sub rax, rbx        ; rax -= rbx
inc rax             ; rax++
dec rax             ; rax--
mul rbx             ; rax * rbx (result in rdx:rax)
div rbx             ; rax / rbx (quotient in rax, remainder in rdx)
neg rax             ; rax = -rax
```

### Bitwise
```asm
and rax, rbx        ; rax &= rbx
or rax, rbx         ; rax |= rbx
xor rax, rbx        ; rax ^= rbx
not rax             ; rax = ~rax
shl rax, 2          ; rax << 2 (shift left)
shr rax, 2          ; rax >> 2 (shift right)
```

### Comparison & Jumps
```asm
cmp rax, rbx        ; Compare (sets flags, doesn't store)
test rax, rax       ; Bitwise AND (sets flags, doesn't store)

jmp label           ; Unconditional jump
je label            ; Jump if equal (ZF=1)
jne label           ; Jump if not equal (ZF=0)
jg label            ; Jump if greater (signed)
jl label            ; Jump if less (signed)
ja label            ; Jump if above (unsigned)
jb label            ; Jump if below (unsigned)
```

### Stack Operations
```asm
push rax            ; rsp -= 8; [rsp] = rax
pop rax             ; rax = [rsp]; rsp += 8
```

### Functions
```asm
call func           ; Push return address, jump to func
ret                 ; Pop return address, jump there
```

## Simple Example Program (NASM syntax)

```asm
section .data
    msg db "Hello", 10      ; String with newline
    len equ $ - msg         ; Length of string

section .text
    global _start

_start:
    ; Write syscall (Linux x64)
    mov rax, 1              ; sys_write
    mov rdi, 1              ; stdout
    mov rsi, msg            ; buffer
    mov rdx, len            ; count
    syscall

    ; Exit syscall
    mov rax, 60             ; sys_exit
    xor rdi, rdi            ; exit code 0
    syscall
```

## Essential Concepts

The Stack:
- Grows downward (high addresses → low)
- `push` decrements rsp, `pop` increments
- Used for local variables, function calls, saved registers

Calling Conventions (System V AMD64 - Linux/Mac):
- Args: `rdi`, `rsi`, `rdx`, `rcx`, `r8`, `r9` (rest on stack)
- Return: `rax`
- Caller-saved: `rax`, `rcx`, `rdx`, `rsi`, `rdi`, `r8`-`r11`
- Callee-saved: `rbx`, `rbp`, `r12`-`r15`

Windows x64:
- Args: `rcx`, `rdx`, `r8`, `r9` (rest on stack)
- Shadow space required (32 bytes)

## Quick Cheatsheet

```
MOV dest, src       ; dest = src
LEA dest, [addr]    ; dest = addr (no memory access)
ADD/SUB dest, src   ; dest +=/−= src
INC/DEC dest        ; dest++/--
MUL/DIV src         ; Multiply/divide rax by src
AND/OR/XOR d, s     ; Bitwise operations
NOT dest            ; Bitwise NOT
SHL/SHR dest, n     ; Shift left/right by n bits
CMP op1, op2        ; Compare (op1 - op2, set flags)
TEST op1, op2       ; Bitwise AND, set flags
JMP/JE/JNE/JG...    ; Jump instructions
PUSH/POP reg        ; Stack operations
CALL/RET            ; Function call/return
NOP                 ; No operation
SYSCALL             ; System call (Linux)
INT 0x80            ; System call (Linux 32-bit)
```

Common Flags:
- ZF (Zero): Result was zero
- SF (Sign): Result was negative
- CF (Carry): Unsigned overflow
- OF (Overflow): Signed overflow

## Getting Started

Tools:
- Assembler: NASM (`nasm -f elf64 file.asm`)
- Linker: ld (`ld -o output file.o`)
- Debugger: GDB or LLDB

Practice:
1. Write "Hello World"
2. Do basic math (add two numbers)
3. Implement a loop (count 1-10)
4. Write a function (add two params)
5. Work with arrays/memory

Resources:
- NASM documentation
- Intel/AMD manuals (detailed but dense)
- OSDev wiki
- best to practice on godbolt.org