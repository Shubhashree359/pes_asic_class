VLSI Physical design for ASICs

Introduction:

Basic Definition:
An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.

RISC-V is an open-source instruction set architecture used to develop custom processors for a variety of applications, from embedded designs to supercomputers.
From Apps to Hardware

Applications: Applications, also known as software applications or simply apps, are programs or software designed to perform specific tasks or functions for end-users. Examples include word processors, web browsers, and games.

System Software: System software refers to a collection of programs and utilities that manage and control a computer system's hardware and provide services to other software applications. It includes the operating system, device drivers, and system utilities.

Compiler: A compiler is a software tool that translates high-level programming code (source code) written by humans into machine code or intermediate code that can be executed directly by a computer's hardware or by a virtual machine.

Assembler: An assembler is a program or tool that translates assembly language code, a low-level human-readable representation of machine code instructions, into machine code that can be executed by a computer's CPU.

RTL (Register-Transfer Level): RTL, or Register-Transfer Level, is a level of hardware description language used to model the behavior of digital circuits at a low level of abstraction. It specifies how data moves between registers and how logic operations are performed.

Hardware: Hardware refers to the physical components of a computer system, including the CPU, memory, storage devices, input/output devices, and other electronic and mechanical components. It is the tangible, physical part of a computer system

LABWORK FOR RISCV TOOLCHAIN

#c program
Writing C program using Leaf editor Writing a c program to find sum of integers from 1 to N

#include<stdio.h>

int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}


Using the gcc compiler, we compiled the program to get the output.
gcc p1.c
./a.out

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/fdb29805-3ef4-415e-88fa-b8b00db6081a)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/e8a37228-7071-4be1-b417-3a18a64bf2c9)

RISCV GCC compiler and disassemble

Using the RISC-V GCC compiler, we compiled the C program.
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o p1.o p1.c
Using ls -ltr p1.c we can check that the object file is created.

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/8565458b-896b-4613-a34e-f9ea96c126a0)

to get dissembled ALP code
use: riscv64-unknown-elf-objdump -d p1.o | less 

In order to view the main section, type /main

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/68f55983-ee86-450e-a60b-e9148178b484)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/d227a66d-ee40-4a39-a3ea-8aaa01657359)

When we use -Ofast optimisation, we can see that the number of instructions have been reduced.


Spike Simulation and Debug:
spike pk p1.o is used to check whether the instructions produced are right to give the correct output.

spike -d pk p1.c is used for debugging.

The contents of the registers can also be viewed.

Press ENTER : to show the first line and successive ENTER to show successive lines reg 0 a2 : to check content of register a2 0th core q : to quit the debug process

Integer Number Representation

 wrIte a C program pg2.c that shows the maximum and minimum values of 64bit Signed numbers.
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/96eb4e06-4d0d-43ef-958a-700c4ab4b786)
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/76630dc7-18d7-486f-b983-5a00d684d2fc)

WrIte a C program pg3.cthat shows the maximum and minimum values of 64bit Unsigned numbers.

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/acd57345-f2f8-47a4-9acc-9f2f049ef21f)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6315bbbb-213d-4631-91f3-fc0b1c88ada3)

Application Binary Interface
Introduction to ABI:
  An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures. The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.

Load, Add and Store Instructions:

Example 1: ld x7, 8(x5)
 *ld is the load double-word instruction.
 *x7 is the destination register.
 *8(x5) is the memory address pointed to by register x5 (base address + offset).
Store Instructions: Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example2: sd x5, 8(x9)
 *sd is the store double-word instruction.
 *x5 is the source register.
 *8(x9) is the memory address pointed to by register x9 (base address + offset).
Add Instructions: Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example 3: add x9, x1, x11

 *add is the add instruction.
 *x9 is the destination register.
 *x1 and x11 are the source registers.

LABWORK:

Write C code in one file and your assembly code in a separate file. In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

C Program - Sum of numbers from 1 to 9:

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/9be2ddeb-25bc-4d28-beb3-5053de0167f9)

Assembly code:

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/aaa724c6-4dae-495b-a149-769056d7cbf2)




running spike commands

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/ef3945d8-4b01-4a7e-871f-47647e8831ad)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/160c57da-3eab-4450-a3ee-a96fddd758b8)

Simulate C Program using Function Call

Compilation: To compile C code and Asseembly file use the command

riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o p3.o p3.c load.s

this would generate object file p3.o

Execution: To execute the object file run the command

spike pk p3.o

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/94daf004-62a8-4b73-9ab3-2fa96812899f)
