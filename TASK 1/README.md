---

# VSDSquadron Mini Internship - Task 1

## Instructor: Kunal Ghosh

Welcome to the repository for the **VSDSquadron Mini Internship**. This internship covers hands-on learning in RISC-V based systems development. In **Task 1**, we explore the differences in assembly code generation between GCC and RISC-V compilers for a simple C program.

---

## Task 1 Overview

### Task 1A - Compile and Execute a Simple C Code using GCC Compiler

#### Steps:
1. **Write a simple C code**: The code below sums numbers from 1 to `n`.
2. **Compile using GCC**: We use the `gcc` compiler to compile the code for a native system.
3. **Observe the Output**: After compiling, the output is executed to display the result.
   
### C Code Example
```c
#include<stdio.h>
int main()
{
  int i, sum = 0; 
  int n = 17; // replace 17 with any value
  for(i = 1; i <= n; ++i)
  {
    sum += i;
  }  
  printf("Sum of numbers from 1 to %d is %d\n", n, sum);
  return 0;
}
```

#### Steps to Compile with GCC:
1. **Create and Edit File**:
    ```bash
    nano sum1ton.c
    ```
    Paste the C code in the file.
    
2. **Compile the C Code**:
    ```bash
    gcc sum1ton.c -o sum1ton
    ```
   
3. **Execute the Compiled Program**:
    ```bash
    ./sum1ton
    ```
    This will print the result: `Sum of numbers from 1 to 17 is 153`.

---

### Task 1B - Compile Using RISC-V GCC and Analyze Assembly Code

In this task, we compile the same C code using the RISC-V toolchain to observe how assembly code is generated. We will also compare two levels of optimization (`-O1` and `-Ofast`) to evaluate the effect of optimization on the generated assembly code.

#### Steps to Install RISC-V Toolchain:
Make sure the RISC-V toolchain is installed. You can refer to your virtual machine setup instructions for more details on how to install this toolchain.

#### Steps to Compile and Analyze:

1. **Compile with RISC-V GCC (Optimization: `-O1`)**:
    ```bash
    riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
    ```

2. **View the Assembly Code with `objdump`**:
    ```bash
    riscv64-unknown-elf-objdump -d sum1ton.o | less
    ```
    This command will display the disassembled RISC-V assembly code of the compiled object file. You can scroll and observe the `main` function’s structure.

3. **Compile with RISC-V GCC (Optimization: `-Ofast`)**:
    ```bash
    riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
    ```

4. **View the Optimized Assembly Code**:
    ```bash
    riscv64-unknown-elf-objdump -d sum1ton.o | less
    ```
    By using `-Ofast`, the code is optimized further, and you’ll notice that the number of assembly instructions generated for the `main` function has reduced significantly.

---

### Summary of Observations:
- **Standard GCC Compilation**: The code compiled and executed successfully, providing the expected sum of numbers.
- **RISC-V GCC Compilation**: The generated assembly code can be analyzed with `objdump`. Different optimization levels (`-O1` vs `-Ofast`) lead to noticeable reductions in the complexity and number of lines in the generated assembly code.
  
#### Example Comparison of Optimizations:
- **`-O1` Compilation**: Provides basic optimization with some performance improvements.
- **`-Ofast` Compilation**: Applies more aggressive optimizations, reducing the number of assembly instructions and potentially improving runtime performance.

---
