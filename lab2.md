### objective
1.Debugging the main function using spark simulation and observing the register values
2.Generating the Object dump file and verify the output with gcc output from lab 1.
## software tools
1.GCC
2.RISCV GNU Compiler
3.Ubuntu
4.Spike Riscv simulator
## Procedure
# STEP1:Compile the code using gcc compiler with the help of following comands
```
gcc sum1ton.c
./a.out
```
# STEP2 : Now compile the same code using risv compiler with the help of following commands
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
spike pk sum1ton.o
```
# STEP3 : Now invoke the object dump using the following commands you can see the assembly ocde and register
```
riscv64-unkown-elf-objdump -d sum1ton.o | less
```
![lab2 -1](https://github.com/user-attachments/assets/32d1a7c2-f5c0-4e59-84a9-85ecfc0688eb)

# STEP4 : Now you will be able to run the codde until which ever line you want using the following commands and you can observe the chnage in values of registers using the following commands
```
until PC 0 100b0
reg 0 a0
reg 0 sp
```
![lab2 -1](https://github.com/user-attachments/assets/0ab348ba-081c-4e44-91ac-523e22a0339a)
--------------------------------------------------------------------------------------------------------##LAB-3
------------------------------------------------------------------------

## TASK-1
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## OBJECTIVE
1.Identifying the type of instruction(R,I,S,B,U,J)
2.Encoding the instructions into 32-bit binary code  for riscv architecture
## PROCEDURE
The following table contains the hexadecimal and binary encodings of each instruction:

| Sl. No. | Instruction            | Type | Hex Encoding | Binary Encoding           |
|---------|------------------------|------|--------------|----------------------------|
| 1       | ADD r4, r5, r6         | R    | 0x00C32333   | 0000000 00101 00110 000 00100 0110011 |
| 2       | SUB r6, r4, r5         | R    | 0x40032333   | 0100000 00100 00101 000 00110 0110011 |
| 3       | AND r5, r4, r6         | R    | 0x00032333   | 0000000 00100 00110 111 00101 0110011 |
| 4       | OR r8, r5, r5          | R    | 0x0002B033   | 0000000 00101 00101 110 01000 0110011 |
| 5       | XOR r8, r4, r4         | R    | 0x000282B3   | 0000000 00100 00100 100 01000 0110011 |
| 6       | SLT r10, r2, r4        | R    | 0x00A32333   | 0000000 00010 00100 010 01010 0110011 |
| 7       | ADDI r12, r3, 5        | I    | 0x00530313   | 000000000101 00011 000 01100 0010011 |
| 8       | SW r3, r1, 4           | S    | 0x00412023   | 000000000100 00001 010 00011 0100011 |
| 9       | SRL r16, r11, r2       | R    | 0x00B282B3   | 0000000 01011 00010 101 10000 0110011 |
| 10      | BNE r0, r1, 20         | B    | 0x00A120E3   | 000000010100 00000 001 00001 1100011 |
| 11      | BEQ r0, r0, 15         | B    | 0xFF5F03E3   | 111111111001 00000 000 00000 1100011 |
| 12      | LW r13, r11, 2         | I    | 0x00B30283   | 000000000010 01011 010 01101 0000011 |
| 13      | SLL r15, r11, r2       | R    | 0x00B302B3   | 0000000 01011 00010 001 01111 0110011 |

This table now includes the hexadecimal and binary encoding for each instruction, providing a complete view of their machine code representation.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## TASK-2
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## OBJECTIVE 
Using verilog netlist and testbench of RISCV core and performing an experiment of functional simulations and observing waveforms
| Operation           | Standard RISC-V ISA | Standard RISC-V ISA (Binary)                              | Hardcoded ISA | Hardcoded ISA (Binary)                               |
|---------------------|----------------------|------------------------------------------------------------|---------------|-------------------------------------------------------|
| ADD R6, R2, R1      | 32'h00110333         | 000000000001 00010 000 00110 0110011                     | 32'h02208300   | 000000100010 00000 100 00000 01100000               |
| SUB R7, R1, R2      | 32'h402083b3         | 010000000010 00000 000 00111 0110011                     | 32'h02209380   | 000000100010 01000 100 10000 01100000               |
| AND R8, R1, R3      | 32'h0030f433         | 000000000011 00000 111 01000 0110011                     | 32'h0230a400   | 000000100011 01000 101 00100 01100000               |
| OR R9, R2, R5       | 32'h005164b3         | 000000000101 00010 110 01001 0110011                     | 32'h02513480   | 000000100101 00010 110 10100 01100000               |
| XOR R10, R1, R4     | 32'h0040c533         | 000000000100 00000 100 01010 0110011                     | 32'h0240c500   | 000000100100 00000 100 11000 01100000               |
| SLT R1, R2, R4      | 32'h0045a0b3         | 000000000100 00010 010 00001 0110011                     | 32'h02415580   | 000000100100 00010 101 01010 01100000               |
| ADDI R12, R4, 5     | 32'h004120b3         | 000000000101 00010 010 01100 0010011                     | 32'h00520600   | 000000100100 00010 010 00010 01100000               |
| BEQ R0, R0, 15      | 32'h00000f63         | 000000000000 00000 000 00000 1100011                     | 32'h00f00002   | 000000000000 00000 000 00000 11000000               |
| SW R3, R1, 2        | 32'h0030a123         | 000000000011 00000 010 00001 0100011                     | 32'h00209181   | 000000100010 00000 010 00001 01100000               |
| LW R13, R1, 2       | 32'h0020a683         | 000000000010 00000 010 01101 0000011                     | 32'h00208681   | 000000100010 00000 010 01100 01100000               |
| SRL R16, R14, R2    | 32'h0030a123         | 000000000011 00000 010 00001 0100011                     | 32'h00271803   | 000000100010 00000 011 00110 01100000               |
| SLL R15, R1, R2     | 32'h002097b3         | 000000000010 00000 111 01111 0110011                     | 32'h00208783   | 000000100010 00000 111 01111 01100000               |


**step1**
1.Download the code from github repo keep it in a folder
2.Run the following commands
![Screenshot (1322)](https://github.com/user-attachments/assets/372e55bb-3bfb-4572-b09a-30c924906d5e)
3.The gtk waveform will pops up 
```
Instruction 1: ADD R6, R2, R1
```
![ins1](https://github.com/user-attachments/assets/cc0b4ec1-593b-4564-a6f5-d6695357f92d)
```
Instruction 2: SUB R7, R1, R2
```
![ins2](https://github.com/user-attachments/assets/80ab79a2-72a4-4805-9d69-60cf8f51a9ca)
```
Instruction 3: AND R8, R1, R3
```
![instr3](https://github.com/user-attachments/assets/140f8d16-82f3-48b8-8758-b817dcbba5ba)
```
Instruction 4: OR R9, R2, R5
```
![instr4](https://github.com/user-attachments/assets/97854d2c-a560-42e7-9248-3d7d4b77c499)
```
Instruction 5: XOR R10, R1, R4
```
![inst5](https://github.com/user-attachments/assets/30c0bd4c-ac17-41cd-8a02-fab1a4c713ab)
```
Instruction 6: SLT R1, R2, R4
```
![inst6](https://github.com/user-attachments/assets/6c5b852d-f732-4e7a-b808-7b25891ebb0a)
```
Instruction 7: ADDI R12, R4, 5
```
![inst7](https://github.com/user-attachments/assets/2b58afd1-0a34-4797-9adf-d851e0e613ed)

```
Instruction 8: BEQ R0, R0, 15
```
![inst8](https://github.com/user-attachments/assets/0d83e9d9-0c99-4e48-bde6-374fd0dafb3d)









