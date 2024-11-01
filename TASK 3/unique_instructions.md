# Unique RISC-V Instructions and Their Types

This document describes 15 unique RISC-V instructions found in the `sum1ton.c` program, including their type, purpose, and breakdown of the 32-bit instruction format.

---

1. **Instruction:** `add x1, x2, x3`
   - **Type:** R-Type
   - **Purpose:** Adds the contents of `x2` and `x3` and stores the result in `x1`.
   - **Format:** `opcode (7 bits) | rd (5 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | funct7 (7 bits)`
   - **Pattern:** `0000000 00011 00010 000 00001 0110011`

2. **Instruction:** `sub x5, x6, x7`
   - **Type:** R-Type
   - **Purpose:** Subtracts the contents of `x7` from `x6` and stores the result in `x5`.
   - **Pattern:** `0100000 00111 00110 000 00101 0110011`

3. **Instruction:** `and x10, x11, x12`
   - **Type:** R-Type
   - **Purpose:** Performs bitwise AND on `x11` and `x12`, storing the result in `x10`.
   - **Pattern:** `0000000 01100 01011 111 01010 0110011`

4. **Instruction:** `or x3, x4, x5`
   - **Type:** R-Type
   - **Purpose:** Performs bitwise OR on `x4` and `x5`, storing the result in `x3`.
   - **Pattern:** `0000000 00101 00100 110 00011 0110011`

5. **Instruction:** `sll x8, x9, x10`
   - **Type:** R-Type
   - **Purpose:** Shifts `x9` left by the value in `x10`, storing the result in `x8`.
   - **Pattern:** `0000000 01010 01001 001 01000 0110011`

6. **Instruction:** `slt x6, x7, x8`
   - **Type:** R-Type
   - **Purpose:** Sets `x6` to 1 if `x7` is less than `x8`.
   - **Pattern:** `0000000 01000 00111 010 00110 0110011`

7. **Instruction:** `addi x1, x2, 10`
   - **Type:** I-Type
   - **Purpose:** Adds immediate value `10` to `x2` and stores the result in `x1`.
   - **Pattern:** `000000000010 00010 000 00001 0010011`

8. **Instruction:** `lw x3, 0(x4)`
   - **Type:** I-Type
   - **Purpose:** Loads a word from memory address `x4 + 0` into `x3`.
   - **Pattern:** `000000000000 00100 010 00011 0000011`

9. **Instruction:** `sw x5, 4(x6)`
   - **Type:** S-Type
   - **Purpose:** Stores the contents of `x5` into memory address `x6 + 4`.
   - **Pattern:** `0000000 00101 00110 010 00000 0100011`

10. **Instruction:** `beq x7, x8, label`
    - **Type:** B-Type
    - **Purpose:** Branches if `x7` equals `x8`.
    - **Pattern:** `0000000 01000 00111 000 label 1100011`

11. **Instruction:** `bne x9, x10, label`
    - **Type:** B-Type
    - **Purpose:** Branches if `x9` does not equal `x10`.
    - **Pattern:** `0000000 01010 01001 001 label 1100011`

12. **Instruction:** `lui x2, 0x1000`
    - **Type:** U-Type
    - **Purpose:** Loads upper immediate `0x1000` into `x2`.
    - **Pattern:** `00000000000000000001 00010 0110111`

13. **Instruction:** `auipc x4, 0x1000`
    - **Type:** U-Type
    - **Purpose:** Adds upper immediate `0x1000` to the PC and stores it in `x4`.
    - **Pattern:** `00000000000000000001 00100 0010111`

14. **Instruction:** `jal x5, label`
    - **Type:** J-Type
    - **Purpose:** Jumps to address `label`, storing return address in `x5`.
    - **Pattern:** `0000000 label 00000 1101111`

15. **Instruction:** `jalr x6, 0(x7)`
    - **Type:** I-Type
    - **Purpose:** Jumps to address `x7 + 0`, storing return address in `x6`.
    - **Pattern:** `000000000000 00111 000 00110 1100111`

---

Each instruction pattern follows the RISC-V ISA standard with exact bit fields specified for each type.
