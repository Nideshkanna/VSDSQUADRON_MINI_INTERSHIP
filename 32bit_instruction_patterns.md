# 32-Bit Instruction Patterns

This file contains the exact 32-bit binary representation for each unique instruction identified in the RISC-V objdump output for `sum1ton.c`.

---

1. **add x1, x2, x3:**  
   `0000000 00011 00010 000 00001 0110011`

2. **sub x5, x6, x7:**  
   `0100000 00111 00110 000 00101 0110011`

3. **and x10, x11, x12:**  
   `0000000 01100 01011 111 01010 0110011`

4. **or x3, x4, x5:**  
   `0000000 00101 00100 110 00011 0110011`

5. **sll x8, x9, x10:**  
   `0000000 01010 01001 001 01000 0110011`

6. **slt x6, x7, x8:**  
   `0000000 01000 00111 010 00110 0110011`

7. **addi x1, x2, 10:**  
   `000000000010 00010 000 00001 0010011`

8. **lw x3, 0(x4):**  
   `000000000000 00100 010 00011 0000011`

9. **sw x5, 4(x6):**  
   `0000000 00101 00110 010 00000 0100011`

10. **beq x7, x8, label:**  
    `0000000 01000 00111 000 label 1100011`

11. **bne x9, x10, label:**  
    `0000000 01010 01001 001 label 1100011`

12. **lui x2, 0x1000:**  
    `00000000000000000001 00010 0110111`

13. **auipc x4, 0x1000:**  
    `00000000000000000001 00100 0010111`

14. **jal x5, label:**  
    `0000000 label 00000 1101111`

15. **jalr x6, 0(x7):**  
    `000000000000 00111 000 00110 1100111`

---

Each binary pattern represents the 32-bit instruction format as per the RISC-V ISA.
