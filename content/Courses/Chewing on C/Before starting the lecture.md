---
tags:
  - C
---

## Why learning C might be uncomfortable
- C language was first introduced in 1972. There have been numerous breakthroughs and improvements, leading to modern programming languages.
- The purpose of C was to make the *UNIX operating system*. This close relation with computer systems might be an obstacle for newcomers.

The reason why C programming language persists today is it's minimalism.
> [!warning] Note
> Minimal learning $\neq$ Ease of Learning

There might be many questions regarding "why it does/doesn't work" due to the lack of understanding in computer systems. It's normal don't worry.

## What is a Computer?
It is simply a calculator which performs sequence of calculations. The main difference between a normal calculator and a computer being it's functionality to automate the calculations.

There are several components of the computer that is worth mentioning here.

- CPU : Central Processing Unit
	- This is where almost all the computations are done
	- Graphic or matrix multiplication related calculations are dealt separately at GPUs
	- Register
		- CPU has it's memory called 'Register's where it reads operations and saves outputs, but it lacks in size.
		- Normally for a 64bit CPU, there are 16 registers, which totals only 128bytes.
	- Cache
		- Cache can help loading data to registers quickly
		- There are three levels of cache being L1~L3 where L1 is fastest and smallest.
- RAM: Random Access Memory
	- Quick accessible memory for the CPU.
	- Slower than CPU registers, but has larger size.
	- RAM is a volatile memory, which means it needs power to maintain it's memory.
- SSD / HDD : Solid State Memory / Hard Disk Drive
	- This is a non-volatile memory to store files and information.
	- But the read and write speed falls way behind the operating speed of the CPU.

## Working Examples
Below is an assembly code example to demonstrate the interaction between CPU and RAM.
```asm
mov eax, 4660 # hex(4660)=0x1234
mov BYTE PTR [rax], 3
```

`eax` and `rax` indicates registers, the difference being how much you are willing to read from the 64bit register. 

> [!info] General Purpose Registers
> General purpose registers (GPRs) have their own names. `eax` and `rax` are one of them. However, `eax` and `rax` indicate the same register, differentiating only in how much bits should be read. `eax` reads the last 32bits whereas `rax` reads full 64bits. This difference is due to the adaptation of 32bit instruction set to a 64bit architecture. (x86_64)

`BYTE PTR` means that the value 3 is saved in one byte space. If you wish to use more than one byte, for instance 4 bytes, we can use `DWORD PTR`. Here, `BYTE` and `DWORD` indicate the different datatypes.


```asm
mov eax, 4660 # hex(4660)=0x1234
mov DWORD PTR [rax], 3
```

The result would be as follows,
```
...
0x1238 : ?
0x1237 : 0
0x1236 : 0
0x1235 : 0
0x1234 : 3
0x1233 : ?
...
```

As shown in the assembly code example, we have to use the registers to record addresses and reference the register when accessing the address. CPU does not allow directly locating the RAM address.

```asm
mov DWORD PTR [4660], 3
```

Note that for 64bit CPU, the register size is also 64bits, i.e. 8bytes. This is because the address is 8bytes for a 64bit system.
## How CPU reads instructions
Then how does CPU know which instructions to run? More specifically, how does CPU know where the instruction is located in the RAM? This is resolved by the *instruction pointer*, a special register which tracks the address of instructions to execute. For the case of Intel 64bit CPU, its name is `RIP`. Whenever CPU fetches an instructions, it updates instruction pointer to the address of next address, normally being the sequential to the previous address.
But when having multiple applications running on the computer, it's sub-optimal to always have the instructions kept in continuous sequences. To make full use of RAM size and increase accessibility from the CPU, *paging* is applied to RAM storage.
*Virtual memory* is how CPU sees instructions in RAM, which is different from *Physical memory*, how memory is actually allocated in RAM. The unit size for the *page* is usually 4kB and each application keeps the *page table* for conversion between virtual and physical memory.

## Summary
- All calculations of the computer is performed in the CPU. To be specific, It is executed in registers, which are 8bytes for 64bit CPUs.
- CPU reads instructions to execute from and writes operation outputs to RAM.
- Running a program means loading stored set of instruction to the memory, then telling CPU the starting address of the program
- CPU caches helps optimize memory access time and frequency
- Each and every program runs using the virtual memory.
- The addresses that CPU references using instruction pointer is not a physical address, but a virtual address.
- The virtual memory address is converted to physical memory address using each program's page table