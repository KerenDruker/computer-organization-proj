## 🖥️ SIMP Processor Simulator and Assembler

# Introduction

This project develops a software-based simulator and assembler for the SIMP processor, a simplified RISC-like processor designed for educational purposes. The programs are crafted in C, showcasing a simulation of processor operations and an assembler that converts assembly code into machine-readable format.

# Project Structure
• **Main.c** - Entry point.

• **Assembler.c** - Source file containing the assembler logic.
    Translates assembly language into binary machine code. It performs label resolution and binary encoding, outputting the memory image file (memin.txt) that serves as the input for the simulator.
    
• **simulator.c** - Source file containing the simulation logic for the SIMP processor.
    Simulates the SIMP processor's fetch-decode-execute cycle, interpreting and executing binary code and writing the results to various output files. It also manages the cycling and timing based on instruction and memory access requirements.
    
# Functionality
•  The SIMP processor contains 16 registers and supports R and I format instructions.
•  The assembler runs through the code twice: first to identify and store labels, and second to translate instructions into machine code.
•  The simulator follows the fetch-decode-execute cycle typical of RISC processors.

# Input and Output Files
•	**memin.txt:** Serves as the input memory file for the simulator, containing the initial state of the processor's memory as a series of 20-bit binary encoded lines, representing the loaded machine code and initial memory state.

•	**memout.txt:** The output memory state file that mirrors the format of memin.txt. It captures the final state of memory after the simulator has processed all instructions.

•	**regout.txt:** Outputs the contents of the processor's registers at the end of the simulation, except for registers R0 and R1. Each line represents one register's contents in 32-bit hexadecimal format.

•	**trace.txt:** Logs each instruction executed during the simulation, listing the program counter, the instruction itself, and the state of all registers before execution, all formatted in hexadecimal.

•	**cycles.txt:** Records the total number of clock cycles consumed during the simulation, providing insight into the performance and efficiency of the simulated processor.

Setup
Compile the project with the following commands:

``` bash

gcc -o sim Main.c simulator.c -I.
gcc -o asm Main.c Assembler.c -I.
```

# Running Instructions
# 🚀 Simulator

``` bash
./sim memin.txt memout.txt regout.txt trace.txt cycles.txt
```

# 📝 Assembler

``` bash
./asm program.asm memin.txt
```

# How to Build
1. Compile the C files using a C compiler, such as GCC:
```bash
gcc -o sim simulator.c Main.c -I.
gcc -o asm Assembler.c Main.c -I.
```
2. Run the assembler to generate the memory input file.
3. Execute the simulator with the generated memory input file.


# Detailed Explanation of Components

## Registers

The SIMP processor features several registers, each serving specific functions:

| Register Number | Register Name | Purpose                                  |
|-----------------|---------------|------------------------------------------|
| 0               | $zero         | Constant zero, always reads as zero      |
| 1               | $imm          | Immediate value, sign-extended           |
| 2 - 15          | $v0 - $ra     | General purpose and special registers    |

## Instruction Formats

### R Format

| Field  | Bit Position | Description       |
|--------|--------------|-------------------|
| opcode | 19:12        | Operation code    |
| rd     | 11:8         | Destination register |
| rs     | 7:4          | Source register 1 |
| rt     | 3:0          | Source register 2 |

### I Format

| Field  | Bit Position | Description       |
|--------|--------------|-------------------|
| opcode | 19:12        | Operation code    |
| rd     | 11:8         | Destination register |
| rs     | 7:4          | Source register 1 |
| imm    | 16 bits      | Immediate value   |

## Supported Instructions

| Opcode | Instruction | Description                                |
|--------|-------------|--------------------------------------------|
| 0      | add         | Adds rs and rt, stores in rd               |
| 1      | sub         | Subtracts rt from rs, stores in rd         |
| ...    | ...         | ...                                        |
| 18     | halt        | Halts execution, exits simulator           |



## Memory Handling: 
Manages the main memory of the processor, simulating reads and writes.

## Error Handling: 
Includes error detection for invalid memory accesses or illegal instructions.

# Detailed Explanation of Code Implementation

## Assembler.c Functionality
Assembler.c translates assembly code for the SIMP processor into machine code. Here’s what each part does based on typical assembler tasks:

Reading Input: It reads assembly instructions from a file, handling labels and directives.

First Pass: Identifies all labels and calculates their addresses, which is crucial for branching and data referencing.

Second Pass: Translates assembly instructions into machine code, replacing labels with their resolved addresses.

Output Generation: Writes the resulting machine code to an output file, typically in a format that the simulator can read directly.
Here’s an example operation you might find based on standard assembler behavior:

Label Handling: It might use a hashmap or dictionary to store label addresses encountered in the first pass, then replace these labels in the second pass with actual numeric addresses.

## Simulator.c Functionality
Simulator.c executes the binary machine code in a simulated environment. Here’s the breakdown of its tasks:

Memory Initialization: Sets up an array or similar data structure to represent memory.

Register Initialization: Initializes registers used by the SIMP processor, including general-purpose and special-purpose registers.

Fetch-Decode-Execute Loop:

Fetch: Retrieves the next instruction from memory based on the program counter.

Decode: Parses the instruction to understand which operation to perform and which registers or memory addresses are involved.

Execute: Performs the operation, which could be arithmetic, logical, data movement, or control flow change.

Output Handling: At the end of simulation, outputs the state of memory and registers, and possibly a trace of execution steps.
An example operation in the fetch-decode-execute loop might look like this:

Branch Handling: For a branch instruction, the condition is evaluated, and the program counter is updated to point to the target instruction if the condition is true.
Integration and Execution

