RISC-V Core Functional Simulation
Task Overview

This task involves performing a functional simulation of a RISC-V Core using a pre-designed Verilog netlist and testbench. The objective is to observe the waveforms for various RISC-V instructions and capture them for analysis.

The simulation is carried out using iverilog for compiling and GTKWave for waveform visualization. The reference GitHub repository containing the Verilog netlist and testbench is named iiitb_rv32i.
Instructions for Functional Simulation

    Clone the Reference Repository Clone the iiitb_rv32i repository that contains the RISC-V Verilog Core and testbench.

git clone <repository_link>

Create a New Directory Create a new directory with your name to organize the files.

mkdir <your_name>
cd <your_name>

Create Verilog Files Create two Verilog files for the core and testbench:

touch maazm_rv32i.v maazm_rv32i_tb.v

Copy the Verilog code for the RISC-V Core and testbench from the reference repository into these files.

Compile and Run Simulation

    Compile the Verilog files with iverilog:

iverilog -o maazm_rv32i maazm_rv32i.v maazm_rv32i_tb.v

Run the compiled code:

    ./maazm_rv32i

This command generates a .vcd file containing the simulation data.

View Simulation in GTKWave

    Open GTKWave to visualize the waveforms:

        gtkwave maazm_rv32i.vcd

        In GTKWave, add relevant signals from the modules to view the instructions and register states.

Observing and Capturing Waveforms

Analyze the waveforms for each instruction and capture screenshots for the following RISC-V instructions:
Instruction	Operation
ADD	ADD R6, R2, R1
SUB	SUB R7, R1, R2
AND	AND R8, R1, R3
OR	OR R9, R2, R5
XOR	XOR R10, R1, R4
SLT	SLT R1, R2, R4
ADDI	ADDI R12, R4, 5
BEQ	BEQ R0, R0, 15
BNE	BNE R0, R1, 20
SLL	SLL R15, R1, R2

For each instruction:

    Capture the state of registers and relevant signals before and after execution.
    Observe changes in values for signals, especially SP (stack pointer) and a0.

Uploading Waveform Snapshots

    Save each waveform screenshot with a descriptive filename (e.g., ADD_waveform.png, SUB_waveform.png, etc.).
    Create a waveforms folder in this directory and move all screenshots into it.
    Commit and push the screenshots to your GitHub repository:

git add waveforms/*.png
git commit -m "Added waveform snapshots for RISC-V functional simulation"
git push origin main
