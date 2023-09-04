# VLSI Physical design for ASICs


## DAY1


### Introduction:

#### Basic Definition:
An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.

RISC-V is an open-source instruction set architecture used to develop custom processors for a variety of applications, from embedded designs to supercomputers.
From Apps to Hardware

#### Applications: 
Applications, also known as software applications or simply apps, are programs or software designed to perform specific tasks or functions for end-users. Examples include word processors, web browsers, and games.

#### System Software: 
System software refers to a collection of programs and utilities that manage and control a computer system's hardware and provide services to other software applications. It includes the operating system, device drivers, and system utilities.

#### Compiler: 
A compiler is a software tool that translates high-level programming code (source code) written by humans into machine code or intermediate code that can be executed directly by a computer's hardware or by a virtual machine.

#### Assembler: 
An assembler is a program or tool that translates assembly language code, a low-level human-readable representation of machine code instructions, into machine code that can be executed by a computer's CPU.

#### RTL (Register-Transfer Level): 
RTL, or Register-Transfer Level, is a level of hardware description language used to model the behavior of digital circuits at a low level of abstraction. It specifies how data moves between registers and how logic operations are performed.

#### Hardware: 
Hardware refers to the physical components of a computer system, including the CPU, memory, storage devices, input/output devices, and other electronic and mechanical components. It is the tangible, physical part of a computer system

### LABWORK FOR RISCV TOOLCHAIN

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

### RISCV GCC compiler and disassemble

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


### Spike Simulation and Debug:
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


## DAY 2


### Application Binary Interface

### Introduction to ABI:

  An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures. The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.

Load, Add and Store Instructions:

#### Example 1: ld x7, 8(x5)

    *ld is the load double-word instruction.
 
    *x7 is the destination register.
 
    *8(x5) is the memory address pointed to by register x5 (base address + offset).
 
Store Instructions: Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

#### Example2: sd x5, 8(x9)

    *sd is the store double-word instruction.
 
    *x5 is the source register.
 
    *8(x9) is the memory address pointed to by register x9 (base address + offset).
 
Add Instructions: Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

#### Example 3: add x9, x1, x11

    *add is the add instruction.
 
    *x9 is the destination register.
 
    *x1 and x11 are the source registers.

### LABWORK:

Write C code in one file and your assembly code in a separate file. In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

C Program - Sum of numbers from 1 to 9:

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/9be2ddeb-25bc-4d28-beb3-5053de0167f9)

#### Assembly code:

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/aaa724c6-4dae-495b-a149-769056d7cbf2)




running spike commands

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/ef3945d8-4b01-4a7e-871f-47647e8831ad)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/160c57da-3eab-4450-a3ee-a96fddd758b8)

### Simulate C Program using Function Call

#### Compilation: To compile C code and Asseembly file use the command

riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o p3.o p3.c load.s

this would generate object file p3.o

#### Execution: To execute the object file run the command

spike pk p3.o

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/94daf004-62a8-4b73-9ab3-2fa96812899f)



## DAY 3

### Introduction to Verilog RTL design and Synthesis

### Introduction to Open-Source Simulator iVerilog

### Introduction to iVerilog Design Testbench

#### Simulator:

 * It is a tool used for simulating the design. It looks for the changes on the input signals to evaluate the outputs.
 * If there is no change in the inputs, the simulator doesn't evaluate the outputs.
 * RTL is checked for adherence to the spec by simulating the design.
 * The tool used here is iverilog .


#### iVerilog :

 * It is an open-source Verilog simulator used for testing and simulating digital circuit designs described in the Verilog hardware description language (HDL).
 * Both the design and the testbench are fed to the simulator and it produces a vcd (value change dump) file.
 * In order to view the vcd file, we use the GTKwave where we can see the wave forms.
   
![Screenshot (9)](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6b031482-8fdb-4be4-890a-97962b7cdb2c)

#### Design

 * It is the actual verilog code or set of verilog codes which ahs the intended functionality to meet with the required specifications.
 * Verilog is used to describe the behavior and structure of digital circuits at different levels of abstraction, from high-level system descriptions down to low-level gate-level 	representations.
 
#### Testbench

 * A testbench is a specialized Verilog module or program used to verify the functionality and behavior of another Verilog module, circuit, or design. Testbenches are essential 		for testing and simulating digital designs before they are synthesized or manufactured as physical chips.
 * It is a setup to apply stimulus to the design to check its functionality.

![Screenshot (11)](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6d76afc4-1a15-48bc-ad9d-bbc41ab3b535)

NOTE:

* design may have one or more primitive inputs and one or more primitive outputs.
* TB doesn't have a primitive inputs or primitive outputs.




## Labs using iVerilog and GTKwave:

### Introduction to Lab:

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

### iVerilog GTKwave Part-1

	cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

	we have loaded the source code along with the testbench code into the iverilog simulator

	iverilog good_mux.v tb_good_mux.v

	We can see that an output file a.out has been created.

	./a.out

	The output of the iverilog, a vcd file, is created which is loaded into the simualtor gtkwave.

  	gtkwave tb_good_mux.vcd
 
 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/5d25fc07-c381-4975-8677-82e8016b69b5)

 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/eb3457de-5bb6-4e7c-a6b1-d6c69d3b57bf)

### iVerilog GTKwave Part-2

	Go to verilog_files directory

	In order to view the contents in the files, gvim tb_good_mux.v -o good_mux.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/dd7c6e05-4ca1-4a32-9752-8a8d6dd077f7)

### Introduction to Yosys and Logic Synthesis

### Introduction to Yosys

#### Synthesizer:

  * It is a tool used for converting RTL design code to netlist.
  * Here, the synthesizer used is Yosys.

#### Yosys

 * It is an open-source framework for Verilog RTL synthesis and formal verification.
 * Yosys provides a collection of tools and algorithms that enable designers to transform high-level RTL (Register Transfer Level) descriptions of digital circuits into optimized gate-level representations suitable for physical implementation on hardware.

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a0c9b87c-b962-4fd3-8570-4ac8ea0029d8)

Design and .lib files are fed to the synthesizer to get a netlist file.

Netlist is the representation of the design in the form of standard cells in the .lib

#### Commands used to perform different opertions:

 * read_verilog to read the design
 * read_liberty to read the .lib file  
 * write_verilog to write out the netlist file

#### To verify the synthesis

 * Netlist along with the tesbench is fed to the iverilog simulator.
 * The vcd file generated is fed to the gtkwave simulator.
 * The output on the simulator must be same as the output observed during RTL simulation.
 * Same RTL testbench can be used as the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

### Introduction to Logic Synthesis

#### Logic Synthesis

 * Logic synthesis is a process in digital design that transforms a high-level hardware description of a digital circuit, typically in a hardware description language (HDL) like Verilog or VHDL, into a lower-level representation composed of logic gates and flip-flops.
 * The goal of logic synthesis is to optimize the design for various criteria such as performance, area, power consumption, and timing.

#### .lib

 * It is a collection of logical modules like And, Or, Not etc.
 * It has different flavors of same gate like 2 input AND gate, 3 input AND gate etc with different performace speed.

#### Why different flavors of gate?

 * In order to make a circuit faster, the clock frequency should be high.
 * For that, the time period of the clock should be as low as possible.

#### In a sequential circuit, clock period depends on:

 * Clock to Q of flip-flop A.
 * Propagation delay of combinational circuit.
 * Setup time of flip-flop B.
 * Tclk > Tcq + Tcomb + Tsetup

#### Why need fast and slow cells?

 * To ensure that there are no HOLD issues at flip-flop B, we require slow cells.
 * For a smaller propagation time, we need faster cells.
 * The collection forms the .lib

### Labs using Yosys and Sky130 PDKs

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

 ## DAY 4:

### Introduction to Timing Dot Libs

### Introduction to Dot Lib

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

### Hierarchical vs Flat Synthesis

#### Hierarchical Synthesis
* Hierarchical synthesis involves dividing the design into logical modules or blocks and synthesizing each module separately.
* These modules can have their own hierarchies, and they communicate through well-defined interfaces
* It enhances reusability, as individual modules can be reused in other designs.
* Supports better scalability for large, complex designs.

#### Steps to Hierarchical Synthesis
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

#### Flattened Synthesis 

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

## Various Flop Coding Styles and Optimization

### D Flip-Flop with Asynchronous Reset

* When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
* Else, on the positive edge of the clock, the stored value is updated at the output.
  
	gvim dff_asyncres_syncres.v

![Screenshot (14)](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/36dcd2fb-d4b4-434d-84a3-9a66bd75f51a)

### D Flip_Flop with Asynchronous Set

* When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
* Else, on positive edge of the clock, the stored value is updated at the output.
  
> gvim dff_async_set.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/4962362b-7f07-4254-ac0a-cad003371ed0)

### D Flip-Flop with Synchronous Reset
* When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
* Else, on the positive edge of the clock, the stored value is updated at the output.
	gvim dff_syncres.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b7f2fac3-651e-436c-9c44-60760bc9ef79)

### D Flip-Flop with Asynchronous Reset and Synchronous Reset

* When the asynchronous resest is high, the output is forced to 0.
* When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
* Else, on the positive edge of the clock, the stored value is updated at the output.
* Here, it is a combination of both synchronous and asynchronous reset DFF.

	gvim dff_asyncres_syncres.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b441b464-a3aa-416e-8f12-f21da72dc827)


## Lab Flop Synthesis Simulations

### D Flip-Flop with Asynchronous Reset

##### Simulation:

* cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* iverilog dff_asyncres.v tb_dff_asyncres.v
* ./a.out
* gtkwave tb_dff_asyncres.vcd

  ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6dcab056-e920-48de-ad3d-2a5eee63d081)

##### Synthesis

* cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
* yosys
* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_asyncres.v
* synth -top dff_asyncres
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/016a4da9-b50e-4431-8aa4-ea5bba4014cf)

### D Flip_Flop with Asynchronous Set

##### Simulation:
    * cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    * iverilog dff_async_set.v tb_dff_async_set.v
    * ./a.out
    * gtkwave tb_dff_async_set.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/8e41c7a7-155e-49f4-aa32-7965486a9af8)

##### Synthesis
   * cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
   * yosys
   * read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   * read_verilog dff_async_set.v
   * synth -top dff_async_set
   * dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   * abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   * show       

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/61b6e81f-31c8-4458-9577-3031161140a0)

### D Flip-Flop with Synchronous Reset

##### Simulation
  * cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  * iverilog dff_syncres.v tb_dff_syncres.v
  * ./a.out
  * gtkwave tb_dff_syncres.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a22b350a-0987-4941-864c-9f9e66c89ef9)

##### Synthesis

  * cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  * yosys
  * read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  * read_verilog dff_syncres.v
  * synth -top dff_syncres
  * dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  * abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  * show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/e6d0c6e6-c7e6-43b8-9fb0-e10edacc7450)

#### interesting optimisation
 * gvim mult_2.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b6ce10e6-bd07-46b1-a7c1-0f53aaeeea39)

 * read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 * read_verilog mult_2.v
 * synth -top mul2

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/45d3065d-00e8-4ed2-84ad-8e8ea8d3d0ec)

 * abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 * show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6b493137-fb21-48a6-ae09-0818f4212ed1)

 * write_verilog -noattr mul2_netlist.v
 * !gvim mul2_netlist.v

##### mul2_netlist.v

	/* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

	module mul2(a, y);
  	input [2:0] a;
  	wire [2:0] a;
  	output [3:0] y;
  	wire [3:0] y;
  	assign y = { a, 1'h0 };
	endmodule

* gvim mult_8.v

 	module mult8 (input [2:0] a , output [5:0] y);
		assign y = a * 9;
	endmodule

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog mult_8.v
* synth -top mult8

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/9e039490-265b-4d3f-ac96-769f78bd9fa1)

* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

 ![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/35c72cbf-a22e-4874-bd14-c22772d51a24)

* write_verilog -noattr mult8_netlist.v
* !gvim mult8_netlist.v

![Screenshot (16)](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b7b9aa7f-0fa9-4a36-a883-554999079668)

## Day 5

### Introduction to Optimisations

#### 1. Combinational Optimisation

 * Combinational optimization is a branch of mathematical optimization that focuses on selecting the best combination of discrete options to optimize a given function.
 * Two methods within computational optimization are:
     * Constant Propagation: This technique identifies and replaces variables or expressions with their constant values, reducing redundancy in code and improving performance.
     * Boolean Optimization: This method simplifies boolean expressions or logic circuits by reducing the number of logical gates or terms while preserving the same logical behavior, 
       which is useful in digital circuit design and logical reasoning.
       
#### 2. Sequential logic optimization

 * Sequential logic optimization is the process of enhancing the performance and efficiency of digital circuits containing flip-flops and state elements.
 * Methods under this optimization umbrella include:
    * ##### Sequential Constant Propagation:
      Identifies and propagates constant values through flip-flops to reduce redundant state transitions.
    * ##### State Optimization:
      Reduces the number of states in finite state machines (FSMs) by merging equivalent states, simplifying the circuit.
    * ##### Sequential Logic Cloning:
      Replicates portions of sequential logic to alleviate bottlenecks and improve circuit throughput.
    * ##### Retiming:
      Adjusts the placement of flip-flops within a circuit to optimize timing, balance critical paths, and enhance overall performance.

### Combinational logic optimizations

##### opt_check.v

* gvim opt_check.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/3382fb1e-388d-4d1a-a398-065a1bb2c200)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog opt_check.v
* synth -top opt_check
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/d724b4b3-4292-46a1-bd6e-b4640133aff0)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/f9be3f47-d85a-41b1-8165-aa3d39c52e4d)

##### opt_check2

* gvim opt_check2.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/eb88677c-6ee2-4a66-8b57-c9379b9b8e81)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.li
* read_verilog opt_check2.v
* synth -top opt_check2
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/31186f1e-10ac-44d0-b8a2-1cdb56013001)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/13eb1d52-aa2b-4be8-89d3-63aeb7984f97)


##### opt_check3

* gvim opt_check3.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a926d58f-9c6e-4324-bde2-32c9d88d6c24)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.li
* read_verilog opt_check3.v
* synth -top opt_check3
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/e6d9a7b6-a0f2-4a0d-8528-05a1ede32f69)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/8961fd44-5cba-4c4b-9ab2-6a95764412c2)

##### opt_check4

* gvim opt_check4.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/bb634201-4720-420c-b013-44d4e82c9269)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.li
* read_verilog opt_check4.v
* synth -top opt_check4
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/83cb40fd-4f01-4106-ab91-3649946ff21b)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/44f7403e-9444-4cb7-a8e3-057bdb2df36e)

##### multiple_module_opt

* gvim multiple_module_opt.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/c38bfcd0-b3f6-42c4-895e-75768148d0a5)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog multiple_module_opt.v
* synth -top multiple_module_opt
* opt_clean -purge
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/3471feb6-1078-4db6-b455-eedda5db761b)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/7b85385a-6a12-45db-9f46-ed27da14e3ba)

### Sequential Logic Optimisations

* dff_const1

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/834a108e-9041-49bc-87ac-1c49d2ce945a)

##### Simulation

* iverilog dff_const1.v tb_dff_const1.v
* /a.out
* gtkwave tb_dff_const1.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/8961a0a4-9e66-4cc8-8fde-18b4413c607c)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const1.v
* synth -top dff_const1
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/cd9d4e9a-b407-4277-9a47-0677b4386368)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/c9e89b50-6419-4e3c-8203-feeef50b48b6)

##### dff_const2
* gvim dff_const2.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/d423c811-eb70-4b2c-8a3e-2292b2888949)

##### Simulation

* iverilog dff_const2.v tb_dff_const2.v
* /a.out
* gtkwave tb_dff_const2.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/eba5786f-9c63-4eca-9a5c-85d32d92e68e)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const2.v
* synth -top dff_const2
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/c14f10a1-997d-4542-b4e0-08804b1c469e) 

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/c9bb1a19-2539-4b43-8b36-35962dbfa2d4)

##### dff_const3

* gvim dff_const3.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/c9d48e6f-c2c4-412c-a8d2-eecd2b78c20f)

##### Simulation

* iverilog dff_const3.v tb_dff_const3.v
* /a.out
* gtkwave tb_dff_const3.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/67d44b8f-a94c-4a40-8eac-8b20ffaac62b)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const3.v
* synth -top dff_const3
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/bcab05e7-755b-4148-8419-0b989a029b6f)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/e5d3340b-77b2-4cd9-ba3f-ab668170fc95)

##### dff_const4

* gvim dff_const4.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b025265e-8ffc-4491-8f7d-356a65b7d423)

##### Simulation

* iverilog dff_const4.v tb_dff_const4.v
* /a.out
* gtkwave tb_dff_const4.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/bf96da52-2fe2-4ff5-99f2-d8464c58d6ef)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const4.v
* synth -top dff_const4
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/9dcd9a7b-1e54-4208-b601-05946941954e)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/e55f2cfd-9503-47b4-8fb0-6f75443f96d1)

##### dff_const5

* gvim dff_const5.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/beadbfb0-72b9-4472-8808-9fa3108ca28e)

##### Simulation

* iverilog dff_const5.v tb_dff_const5.v
* /a.out
* gtkwave tb_dff_const5.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/f83de1ad-8306-48dc-9c2c-50df8c5136fe)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog dff_const5.v
* synth -top dff_const5
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a83ffce7-f47d-4194-a6ad-720e8c1ca463)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/edcc43e8-dbad-47e6-aeb4-dbeb21a6d008)

### Sequential Optimisations for Unused Outputs

##### counter_opt

* gvim counter_opt.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/9566f6a7-5fc1-49f8-8b7c-97d1d8012a1d)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog counter_opt.v
* synth -top counter_opt
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/2b512f88-5d65-4394-b3fc-e6f1b888c1a9)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/ad7d44a7-08f7-4011-8600-3d469c761632)

##### counter_opt2

* gvim counter_opt2.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/0e44ed44-fc92-4f78-b832-53f31ddcb0b1)

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog counter_opt2.v
* synth -top counter_opt2
* dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/bb89ca28-32e0-4651-ab6f-7b3b305d1d73)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/1f6325bf-11c7-41e6-8577-fcd2e74f89e3)

## Day 6

### GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements

#### GLS Concepts And Flow Using Iverilog

##### Gate Level Simualtion
* Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
* It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
* This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
* We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b8a9e32d-1ec5-45b9-b97f-05e4ffbed369)


##### Synthesis-Simulation Mismatch

* A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired  behavior of the circuit after it has been synthesized.
* This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
* This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.

##### Blocking Statements
* Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.
* ###### Example:
 	a = b + c; // b and c must be known before calculating 'a'

##### Non-Blocking Statements 
* Non-blocking assignments are used to model concurrent signal updates, where all assignments are evaluated simultaneously and then scheduled to be updated at the end of the time step.
* ###### Example:
	always @(posedge clk)
 	 begin
  	 b <= a; // Concurrently scheduled assignment
    	 c <= b; // Concurrently scheduled assignment
  	end
  
### Caveats With Blocking Statements

#### Caveats with blocking statements in hardware description languages like Verilog include:

* ##### Sequential Execution:
Blocking statements execute sequentially, which may not accurately represent concurrent hardware behavior in the design.

* ##### Order Dependency: 
The order of blocking statements can affect simulation results, leading to race conditions or unintended behavior.

* ##### Combinational Logic Only: 
Blocking statements are primarily used for modeling combinational logic, making them less suitable for sequential or synchronous logic.

* ##### Limited for Testbenches: 
In testbench code, excessive use of blocking statements can lead to simulation race conditions that don't reflect real-world hardware behavior.

* ##### Initialization Issues: 
In some cases, initializing variables with blocking assignments can lead to unexpected results due to order-dependent initialization.

To mitigate these issues, designers often use non-blocking statements for modeling sequential logic and adopt good coding practices to minimize order dependencies and improve code clarity.

### Labs on GLS and Synthesis-Simulation Mismatch

##### ternary_operator_mux.v
* gvim teranry_operator_mux.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6e33d18b-ca62-4e4a-b494-6f6943f7b0b9)

##### Simulation

* iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
* ./a.out
* gtkwave tb_ternary_operator_mux.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/02bd8481-bd8b-459c-a3d4-907ae7b2efaa)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog ternary_operator_mux.v
* synth -top ternary_operator_mux
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/a8a46f44-1538-479c-8220-ce3d0df74336)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/406f7fe8-6a01-41cd-987c-cedf602907d7)

#### GLS to Gate-Level Simulation

* iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_netlist.v tb_ternary_operator_mux.v
* ./a.out
* gtkwave tb_ternary_operator_mux.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/96e76c9f-9dac-48b4-8063-4f247e55c547)

##### bad_mux
* gvim bad_mux.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/2dd3d004-e1f4-46d6-b2eb-ae5be9d70367)

##### Simualtion

* iverilog bad_mux.v tb_bad_mux.v
* ./a.out
* gtkwave tb_bad_mux.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/6df5ae00-828b-488a-8291-1837266b064f)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog bad_mux.v
* synth -top bad_mux
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/65b14c90-d6ce-49f3-b03d-a119d25ce3c5)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/e8fabdf7-7c5c-43f4-b200-8bec100a2ed7)

### GLS to Gate-Level Simulation

* iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
* ./a.out
* gtkwave tb_bad_mux.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/ca4b0059-8591-4d9b-a1d3-cda415351f6a)

## Labs on Synth-Sim Mismatch for Blocking Statement

##### blocking_caveat

* gvim blocking_caveat.v

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/0d4db267-dcfe-4bb0-a6e6-8a9739cb5832)

##### Simualtion

* iverilog blocking_caveat.v tb_blocking_caveat.v
* ./a.out
* gtkwave tb_blocking_caveat.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/3d1df36a-7441-435b-82ba-2d4d3c93ed11)

##### Synthesis

* read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* read_verilog blocking_caveat.v
* synth -top blocking_caveat
* abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
* show

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b5ae9a53-9591-4c61-9ffa-67f45d319e79)

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/b52b1179-2dfd-4ba7-b9e1-11fae7171f6c)

### GLS to Gate-Level Simulation

* iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
* ./a.out
* gtkwave tb_blocking_caveat.vcd

![image](https://github.com/Shubhashree359/pes_asic_class/assets/142501263/19745cee-e4d6-42cf-8273-fd0dcf0bf598)












