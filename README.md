## 🖥️ SIMP Processor Simulator and Assembler

# Introduction

This project develops a software-based simulator and assembler for the SIMP processor, a simplified RISC-like processor designed for educational purposes. The programs are crafted in C, showcasing a simulation of processor operations and an assembler that converts assembly code into machine-readable format.

# Project Structure
•	Main.c - Entry point.

•	Assembler.c - Source file containing the assembler logic.
    Translates assembly language into binary machine code. It performs label resolution and binary encoding, outputting the memory image file (memin.txt) that serves as the input for the simulator.
    
•	simulator.c - Source file containing the simulation logic for the SIMP processor.
    Simulates the SIMP processor's fetch-decode-execute cycle, interpreting and executing binary code and writing the results to various output files. It also manages the cycling and timing based on instruction and memory access requirements.
    

# Input and Output Files
•	memin.txt: Serves as the input memory file for the simulator, containing the initial state of the processor's memory as a series of 20-bit binary encoded lines, representing the loaded machine code and initial memory state.

•	memout.txt: The output memory state file that mirrors the format of memin.txt. It captures the final state of memory after the simulator has processed all instructions.

•	regout.txt: Outputs the contents of the processor's registers at the end of the simulation, except for registers R0 and R1. Each line represents one register's contents in 32-bit hexadecimal format.

•	trace.txt: Logs each instruction executed during the simulation, listing the program counter, the instruction itself, and the state of all registers before execution, all formatted in hexadecimal.

•	cycles.txt: Records the total number of clock cycles consumed during the simulation, providing insight into the performance and efficiency of the simulated processor.
