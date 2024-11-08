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
![image](https://github.com/user-attachments/assets/e292137d-acfe-4752-bd6f-c776fb9a2acd)

