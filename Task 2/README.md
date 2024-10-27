
---

# Task 2 - RISC-V SPIKE Simulation, Debugging, and Stack Analysis

## Overview:

In **Task 2**, we compiled and simulated the `sum1ton` code with the RISC-V SPIKE simulator, using both regular and debugging modes to analyze register values and stack pointer behavior. This task focuses on examining the differences in register and stack pointer values before and after execution to understand how the RISC-V architecture manages memory and execution flow.

## Objectives:

1. Compile the `sum1ton` code with the RISC-V toolchain.
2. Simulate and observe the output in SPIKE.
3. Use SPIKE in debugging mode to analyze register values and stack pointer changes step-by-step.

---

## Steps:

### Step 1: Compile the `sum1ton` Code with RISC-V GCC

1. **Compile the `sum1ton.c` Code**:
   - Command:
     ```bash
     riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
     ```
   - This generates an executable `sum1ton.o` with `-O1` optimization.

2. **Verify Compilation Output**:
   - Command to view disassembled code:
     ```bash
     riscv64-unknown-elf-objdump -d sum1ton.o | less
     ```
   - This command provides the assembly output, which we use to observe the compiled code structure.

---

### Step 2: Run the Compiled Code Using SPIKE

1. **Run SPIKE Simulation**:
   - Command:
     ```bash
     spike pk sum1ton.o
     ```
   - This command executes the code in SPIKE, simulating the behavior of the RISC-V ISA.

2. **Observe Output**:
   - Check the output to verify the program execution and expected results.

---

### Step 3: Analyze Code with SPIKE in Debugging Mode

1. **Run SPIKE in Debugging Mode**:
   - Start SPIKE with debugging enabled to allow for step-by-step execution:
     ```bash
     spike -d pk sum1ton.o
     ```

2. **Step-by-Step Execution**:
   - Begin execution by setting the initial instruction address, then step through the code by pressing `enter`.
   - During execution, we inspected register and stack values at key points.

3. **Register `a0` Observations**:
   - Before execution of the main function, observe the value of the register `a0`.
   - After running the code up to the `main` function’s completion, observe the updated `a0` value.
   - These observations indicate changes in `a0` resulting from the summation logic in `sum1ton`.

4. **Stack Pointer (`sp`) Observations**:
   - Check the `sp` (stack pointer) register value at the start:
     - Initial `sp` value: `0x0000003ffffffb50`
   - After executing a few instructions, observe the `sp` again:
     - Updated `sp` value: `0x0000003ffffffb40`
   - **Difference Observed**: The `sp` value has shifted by 0x10 bytes, indicating memory allocation for local variables or call frames during execution.

5. **Continue Execution**:
   - Step through each instruction by pressing `enter`, monitoring the changes in registers and stack pointer values as the code progresses.

---

## Observations and Analysis:

1. **Register `a0`**:
   - The register `a0` is used to hold values related to function calls and return values. By stepping through in SPIKE's debug mode, we observed `a0` holding the accumulated sum at specific stages.

2. **Stack Pointer (`sp`) Dynamics**:
   - The `sp` value changed from `0x0000003ffffffb50` to `0x0000003ffffffb40`, indicating a decrease as memory was allocated on the stack.
   - The difference of `0x10` bytes suggests usage of stack memory for variables or function call frames, typical in RISC-V's calling convention and stack management.

---

## Summary:

This task provided insight into the low-level behavior of the RISC-V ISA through SPIKE debugging. By observing `a0` and `sp` register values, we could trace stack allocation and register usage, demonstrating effective memory and register management in RISC-V for a simple summation program.

---
