
---

# Task 3 - RISC-V Instruction Analysis

## Objective

In this task, we dive deeper into the RISC-V Instruction Set Architecture (ISA) by:
1. Listing and understanding various RISC-V instruction types.
2. Identifying 15 unique RISC-V instructions from the disassembly of the `sum1ton` application code.
3. Analyzing each instruction to derive its exact 32-bit binary pattern based on RISC-V encoding.
4. Documenting and uploading these 32-bit instruction patterns on GitHub.

---

## Step 1: RISC-V Instruction Types

The RISC-V ISA classifies instructions into five main types based on their format and functionality:

- **R-Type** (Register type): Used for register-register operations.
  - Example: `add`, `sub`, `and`
  - Structure: `opcode (7 bits) | rd (5 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | funct7 (7 bits)`

- **I-Type** (Immediate type): Used for immediate values or load instructions.
  - Example: `addi`, `lb`, `jalr`
  - Structure: `opcode (7 bits) | rd (5 bits) | funct3 (3 bits) | rs1 (5 bits) | imm[11:0] (12 bits)`

- **S-Type** (Store type): Used for store instructions.
  - Example: `sw`, `sh`, `sb`
  - Structure: `opcode (7 bits) | imm[4:0] (5 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | imm[11:5] (7 bits)`

- **B-Type** (Branch type): Used for conditional branch instructions.
  - Example: `beq`, `bne`, `blt`
  - Structure: `opcode (7 bits) | imm[4:1|11] (5 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | imm[12|10:5] (7 bits)`

- **U-Type** (Upper Immediate type): Used for instructions with upper immediate values.
  - Example: `lui`, `auipc`
  - Structure: `opcode (7 bits) | rd (5 bits) | imm[31:12] (20 bits)`

- **J-Type** (Jump type): Used for jump instructions.
  - Example: `jal`
  - Structure: `opcode (7 bits) | rd (5 bits) | imm[20|10:1|11|19:12] (20 bits)`

---

## Step 2: Identifying 15 Unique Instructions from the `sum1ton` Code

After disassembling `sum1ton.o` using the command below, we identified 15 unique instructions used in the program:

```bash
riscv64-unknown-elf-objdump -d sum1ton.o | less
```

### Unique Instructions

1. `add`
2. `addi`
3. `sub`
4. `mul`
5. `div`
6. `beq`
7. `bne`
8. `jal`
9. `jalr`
10. `lui`
11. `auipc`
12. `sw`
13. `lw`
14. `sb`
15. `sh`

---

## Step 3: Mapping Instructions to 32-Bit Instruction Codes

For each instruction, we detail the exact 32-bit binary pattern based on its instruction type and fields. Here’s an example of the encoding for each:

1. **add x1, x2, x3**
   - R-Type
   - `opcode: 0110011 | funct3: 000 | funct7: 0000000`
   - Binary: `0000000 00011 00010 000 00001 0110011`

2. **addi x1, x2, 5**
   - I-Type
   - `opcode: 0010011 | funct3: 000`
   - Binary: `000000000101 00010 000 00001 0010011`

3. **sub x4, x5, x6**
   - R-Type
   - `opcode: 0110011 | funct3: 000 | funct7: 0100000`
   - Binary: `0100000 00110 00101 000 00100 0110011`

4. **mul x7, x8, x9**
   - R-Type
   - `opcode: 0110011 | funct3: 000 | funct7: 0000001`
   - Binary: `0000001 01001 01000 000 00111 0110011`

5. **div x10, x11, x12**
   - R-Type
   - `opcode: 0110011 | funct3: 100 | funct7: 0000001`
   - Binary: `0000001 01100 01011 100 01010 0110011`

6. **beq x13, x14, label**
   - B-Type
   - `opcode: 1100011 | funct3: 000`
   - Example binary pattern: `imm[12|10:5] 00000 rs2 rs1 funct3 imm[4:1|11] opcode`

7. **bne x15, x16, label**
   - B-Type
   - `opcode: 1100011 | funct3: 001`
   - Example binary pattern: `imm[12|10:5] 00000 rs2 rs1 funct3 imm[4:1|11] opcode`

8. **jal x17, offset**
   - J-Type
   - `opcode: 1101111`
   - Example binary pattern: `imm[20|10:1|11|19:12] 00000 rd opcode`

9. **jalr x18, x19, 0**
   - I-Type
   - `opcode: 1100111 | funct3: 000`
   - Example binary pattern: `imm[11:0] rs1 funct3 rd opcode`

10. **lui x20, 0x10000**
    - U-Type
    - `opcode: 0110111`
    - Binary: `0000000000000001 00000 0110111`

11. **auipc x21, 0x20000**
    - U-Type
    - `opcode: 0010111`
    - Binary: `0000000000000010 00000 0010111`

12. **sw x22, offset(x23)**
    - S-Type
    - `opcode: 0100011 | funct3: 010`
    - Example binary pattern: `imm[11:5] rs2 rs1 funct3 imm[4:0] opcode`

13. **lw x24, offset(x25)**
    - I-Type
    - `opcode: 0000011 | funct3: 010`
    - Example binary pattern: `imm[11:0] rs1 funct3 rd opcode`

14. **sb x26, offset(x27)**
    - S-Type
    - `opcode: 0100011 | funct3: 000`
    - Example binary pattern: `imm[11:5] rs2 rs1 funct3 imm[4:0] opcode`

15. **sh x28, offset(x29)**
    - S-Type
    - `opcode: 0100011 | funct3: 001`
    - Example binary pattern: `imm[11:5] rs2 rs1 funct3 imm[4:0] opcode`

> **Note:** Replace specific registers and immediate values with their actual values in binary for a complete 32-bit pattern. The `label` and `offset` values depend on specific code locations.

---

## Step 4: Upload 32-Bit Patterns on GitHub

The identified binary patterns for each instruction type have been saved as `.md` files and uploaded to the GitHub repository under a `task3` directory

For **Step 4**, here’s a complete guide for creating and uploading the identified 32-bit binary instruction patterns to GitHub. This step involves creating two additional files: one to document the 15 unique RISC-V instructions and another containing their 32-bit patterns.

---

## Step 4: Document and Upload 32-Bit Patterns on GitHub

### Preparing Files for GitHub

1. **Create Documentation Files:**
   - In the `task3` folder, create two files: 
     - `unique_instructions.md`: This file describes the 15 unique instructions with their type, purpose, and breakdown of opcode and fields.
     - `32bit_instruction_patterns.md`: This file contains the exact 32-bit patterns derived for each instruction, presented in binary format.

2. **Example Content for `unique_instructions.md`:**
   - **Instruction:** `add x1, x2, x3`
     - **Type:** R-Type
     - **Purpose:** Performs addition of two registers
     - **Format:** `opcode (7 bits) | rd (5 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | funct7 (7 bits)`
     - **Pattern:** `0000000 00011 00010 000 00001 0110011`
   
   - Include similar entries for the remaining 14 instructions.

3. **Example Content for `32bit_instruction_patterns.md`:**
   - For each instruction, write out the binary pattern in 32-bit format.
   - Example for `add x1, x2, x3`:  
     ```plaintext
     0000000 00011 00010 000 00001 0110011
     ```

4. **Push Files to GitHub:**
   - In your local repository, add and commit the files:
     ```bash
     git add task3/unique_instructions.md task3/32bit_instruction_patterns.md
     git commit -m "Add RISC-V instruction analysis and 32-bit patterns for Task 3"
     ```

   - Push the changes to your GitHub repository:
     ```bash
     git push origin main
     ```



---

