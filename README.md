VLSI Physical design for ASICs


DAY1


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


DAY 2


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



DAY 3

Introduction to Verilog RTL design and Synthesis

Introduction to Open-Source Simulator iVerilog

Introduction to iVerilog Design Testbench

Simulator:

 * It is a tool used for simulating the design. It looks for the changes on the input signals to evaluate the outputs.
 * If there is no change in the inputs, the simulator doesn't evaluate the outputs.
 * RTL is checked for adherence to the spec by simulating the design.
 * The tool used here is iverilog .


iVerilog :

 * It is an open-source Verilog simulator used for testing and simulating digital circuit designs described in the Verilog hardware description language (HDL).
 * Both the design and the testbench are fed to the simulator and it produces a vcd (value change dump) file.
 * In order to view the vcd file, we use the GTKwave where we can see the wave forms.
   
![Screenshot (9)](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6b031482-8fdb-4be4-890a-97962b7cdb2c)

Design

 * It is the actual verilog code or set of verilog codes which ahs the intended functionality to meet with the required specifications.
 * Verilog is used to describe the behavior and structure of digital circuits at different levels of abstraction, from high-level system descriptions down to low-level gate-level 	representations.
 
Testbench

 * A testbench is a specialized Verilog module or program used to verify the functionality and behavior of another Verilog module, circuit, or design. Testbenches are essential 		for testing and simulating digital designs before they are synthesized or manufactured as physical chips.
 * It is a setup to apply stimulus to the design to check its functionality.

![Screenshot (11)](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6d76afc4-1a15-48bc-ad9d-bbc41ab3b535)

NOTE:

* design may have one or more primitive inputs and one or more primitive outputs.
* TB doesn't have a primitive inputs or primitive outputs.




Labs using iVerilog and GTKwave:

Introduction to Lab:

     Make a directory named vsd mkdir vsd.
 
     cd vsd.
 
     git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
 
     Creates a folder called sky130RTLDesignAndSynthesisWorkshop in the vsd directory.
 	
 You could see two folders under sky130RTLDesignAndSynthesisWorkshop
  
  i)  my_lib: It contains all the standard cell libraries and verilog module
  
 ii) verilog_files: It contains all the source code and testbench required for the lab
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a6b3e673-f9df-468e-b4c8-05975fcab882)

       lib : contains sky130 standard cell library used for our synthesis

       verilog_model : contains all the standard cell verilog modules of the standard cells contained in the .lib

iVerilog GTKwave Part-1

	cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

	we have loaded the source code along with the testbench code into the iverilog simulator

	iverilog good_mux.v tb_good_mux.v

	We can see that an output file a.out has been created.

	./a.out

	The output of the iverilog, a vcd file, is created which is loaded into the simualtor gtkwave.

  	gtkwave tb_good_mux.vcd
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/5d25fc07-c381-4975-8677-82e8016b69b5)

 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/eb3457de-5bb6-4e7c-a6b1-d6c69d3b57bf)

iVerilog GTKwave Part-2

	Go to verilog_files directory

	In order to view the contents in the files, gvim tb_good_mux.v -o good_mux.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/dd7c6e05-4ca1-4a32-9752-8a8d6dd077f7)

Introduction to Yosys and Logic Synthesis

Introduction to Yosys

Synthesizer:

  * It is a tool used for converting RTL design code to netlist.
  * Here, the synthesizer used is Yosys.

Yosys

 * It is an open-source framework for Verilog RTL synthesis and formal verification.
 * Yosys provides a collection of tools and algorithms that enable designers to transform high-level RTL (Register Transfer Level) descriptions of digital circuits into optimized gate-level representations suitable for physical implementation on hardware.

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a0c9b87c-b962-4fd3-8570-4ac8ea0029d8)

Design and .lib files are fed to the synthesizer to get a netlist file.

Netlist is the representation of the design in the form of standard cells in the .lib

Commands used to perform different opertions:

 * read_verilog to read the design
 * read_liberty to read the .lib file  
 * write_verilog to write out the netlist file

To verify the synthesis

 * Netlist along with the tesbench is fed to the iverilog simulator.
 * The vcd file generated is fed to the gtkwave simulator.
 * The output on the simulator must be same as the output observed during RTL simulation.
 * Same RTL testbench can be used as the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

Introduction to Logic Synthesis

Logic Synthesis

 * Logic synthesis is a process in digital design that transforms a high-level hardware description of a digital circuit, typically in a hardware description language (HDL) like Verilog or VHDL, into a lower-level representation composed of logic gates and flip-flops.
 * The goal of logic synthesis is to optimize the design for various criteria such as performance, area, power consumption, and timing.

.lib

 * It is a collection of logical modules like And, Or, Not etc.
 * It has different flavors of same gate like 2 input AND gate, 3 input AND gate etc with different performace speed.

Why different flavors of gate?

 * In order to make a circuit faster, the clock frequency should be high.
 * For that, the time period of the clock should be as low as possible.

In a sequential circuit, clock period depends on:

 * Clock to Q of flip-flop A.
 * Propagation delay of combinational circuit.
 * Setup time of flip-flop B.
 * Tclk > Tcq + Tcomb + Tsetup

Why need fast and slow cells?

 * To ensure that there are no HOLD issues at flip-flop B, we require slow cells.
 * For a smaller propagation time, we need faster cells.
 * The collection forms the .lib

Labs using Yosys and Sky130 PDKs

Steps to realize good_mux(design) in terms of standard cells avilable in library sky130_fd_sc_hd__tt_025C_1v80.lib

* Go to verilog_files directory

	cd
 	cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
	Invoke yosys by using the command yosys
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/336c566a-8233-4eaa-9155-922a6d3e809f)

* To read the library
	read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

* To read the design
	read_verilog good_mux.v

* To syntheis the module
	synth -top good_mux

 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/beace35b-b2ce-4c79-86d0-05b803e41ae9)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/2738dc6b-8308-4a57-8d02-0b15213dabcb)

* To generate the netlist
	abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/fcbb19a2-9db6-46e1-988d-d866c2937a9b)


It gives a report of what cells are used and the number of input and output signals.

* To see the logic realised
	show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/c2895ca0-72de-4ae9-875b-1b4a4b7ac122)

The mux is completely realised in the form of sky130 library cells.

To write the netlist
	write_verilog good_mux_netlist.v
	!gvim good_mux_netlist.v

To view a simplified code
	write_verilog -noattr good_mux_netlist.v
	!gvim good_mux_netlist.v


![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/70ae6c3a-4017-427d-8a76-70bb55e16051)

	/* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

	module good_mux(i0, i1, sel, y);
  	wire _0_;
  	wire _1_;
  	wire _2_;
  	wire _3_;
  	input i0;
  	wire i0;
  	input i1;
  	wire i1;
  	input sel;
  	wire sel;
  	output y;
  	wire y;
  	sky130_fd_sc_hd__mux2_1 _4_ (
    	  .A0(_0_),
    	  .A1(_1_),
    	  .S(_2_),
    	  .X(_3_)
  	);
  	assign _0_ = i0;
  	assign _1_ = i1;
  	assign _2_ = sel;
  	assign y = _3_;
	endmodule

 DAY 4:

Introduction to Timing Dot Libs

Introduction to Dot Lib

To view the contents in the .lib
	gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/965cb6d1-b6d2-4cab-b3a6-0b72f3ec94a5)

to dissable the colour 
	:sy off
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/1be8b575-521c-46c9-885c-5fdb089d61c7)

In the first line in the file library ("sky130_fd_sc_hd__tt_025C_1v80")  :

* tt : indicates variations due to process and here it indicates Typical Process.
* 025C : indicates the variations due to temperatures where the silicon will be used.
* 1v80 : indicates the variations due to the voltage levels where the silicon will be incorporated.

It also displays the units of various parameters.

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/14d658be-8f9e-495c-adc8-37481a251db2)

* it gives the features of the cells
* To enable line number :se nu
* To view all the cells :g//
* To view any instance :/instance
* Since there are 5 inputs, for all the 32 possible combinations, it gives the delay, power and all the other parameters for each cell.

Hierarchical vs Flat Synthesis

Hierarchical Synthesis

Hierarchical synthesis involves dividing the design into logical modules or blocks and synthesizing each module separately.

These modules can have their own hierarchies, and they communicate through well-defined interfaces

It enhances reusability, as individual modules can be reused in other designs.

Supports better scalability for large, complex designs.

Steps to Hierarchical Synthesis
* Go to verilog_files directory
* once you get to verilog_files directory, Invoke yosys by using the command yosys

The file we used in this lab is multiple_modules.v

* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* gvim multiple_modules.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/1ef5f65a-24b0-440d-9e25-d3213aaa3378)

* multiple_modules instantiates sub_module1 and sub_module2
* Launch yosys
* read the library file read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read the verilog file  read_verilog multiple_modules.v
* synth -top multiple_modules to set it as top module

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/fb6db570-23b2-4707-9c5c-0c96f9e66d7f)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/f553e049-bd89-4e25-860c-7c85d3086521)

* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* To view the netlist show multiple_modules

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b232bc58-e737-4d4c-a289-c89ee03abb11)

* Here it shows sub_module1 and sub_module2 instead of AND gate and OR gate.
* write_verilog -noattr multiple_modules_hier.v
* !gvim multiple_modules_hier.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/de95b7b7-3f1d-4d8f-956a-7a2f6ae67fcc)

/* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

module multiple_modules(a, b, c, y);
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  wire net1;
  output y;
  wire y;
  sub_module1 u1 (
    .a(a),
    .b(b),
    .y(net1)
  );
  sub_module2 u2 (
    .a(net1),
    .b(c),
    .y(y)
  );
endmodule

module sub_module1(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__and2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule

module sub_module2(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__or2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule

Flattened Synthesis 

Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation. This means that the entire design is synthesized as a single unit, without preserving the modular organization present in the original high-level description.

* Launch yosys
* read the library file read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read the verilog file  read_verilog multiple_modules.v
* synth -top multiple_modules to set it as top module
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* flatten to write out a flattened netlist
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/795589c4-cfec-4a83-a163-48e0bb68450d)

* write_verilog -noattr multiple_modules_flat.v
* !gvim multiple_modules_flat.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/7c8f363d-8e83-4d52-9a43-a7b3aaf3fc30)
![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/5bf69039-3240-4082-8fc1-3a84cdcefb7e)

Various Flop Coding Styles and Optimization

D Flip-Flop with Asynchronous Reset

* When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
* Else, on the positive edge of the clock, the stored value is updated at the output.
  
	gvim dff_asyncres_syncres.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/4962362b-7f07-4254-ac0a-cad003371ed0)

D Flip-Flop with Synchronous Reset
* When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
* Else, on the positive edge of the clock, the stored value is updated at the output.
	gvim dff_syncres.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b7f2fac3-651e-436c-9c44-60760bc9ef79)

D Flip-Flop with Asynchronous Reset and Synchronous Reset

* When the asynchronous resest is high, the output is forced to 0.
* When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
* Else, on the positive edge of the clock, the stored value is updated at the output.
* Here, it is a combination of both synchronous and asynchronous reset DFF.

	gvim dff_asyncres_syncres.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b441b464-a3aa-416e-8f12-f21da72dc827)


Lab Flop Synthesis Simulations

D Flip-Flop with Asynchronous Reset

Simulation:

* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* iverilog dff_asyncres.v tb_dff_asyncres.v
* ./a.out
* gtkwave tb_dff_asyncres.vcd

  ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6dcab056-e920-48de-ad3d-2a5eee63d081)

Synthesis

* cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* yosys
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_asyncres.v
* synth -top dff_asyncres
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/016a4da9-b50e-4431-8aa4-ea5bba4014cf)

D Flip_Flop with Asynchronous Set

* Simulation:
    * cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    * iverilog dff_async_set.v tb_dff_async_set.v
    * ./a.out
    * gtkwave tb_dff_async_set.vcd
       
