# ASIC DESIGN LAB REPOS 

<tr></tr>

****The following tools are used in lab****

Software Tools:

1.GCC (GNU Compiler Collection)

2.RISC-V GNU Compiler Toolchain

3.Spike RISC-V Simulator

4.Ubuntu OS

5.Oracle Virtual box

<details>
<summary>Lab 1</summary>
<br>
  
WRITING A C PROGRAM FOR SUM OF NUMBERS AND COMPILING THE CODE USING GCC and RISC-V COMPILER AND COMPARING THEIR OUTPUTs
--------------------------------------------------------------------------------------------------------------------------------
# the following code snippet is compiled using gcc and riscv compiler
## **TASK1: Compile code using GCC compiler**
  
![image](https://github.com/user-attachments/assets/3d7fa23e-e6fc-4795-88cd-e316d5436d70)

the above picture contains c code for sum of numbers from 1 to n 

the output of the code is shown below:

![task1](https://github.com/user-attachments/assets/5168e01b-4f22-4d77-b84d-5152d69ce47d)


#### **TASK2: Compile code using RISC-V GNU compiler**

# now compile the same code using RISC-V GNU Compiler 
compile the code using following command 
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sumton.o sumton.c
```
run the compiled code 
```riscv64-unknown-elf-objdump -d sumton.o | less
```
after that search for main function and we can see that it will take 15 steps
![task-o1](https://github.com/user-attachments/assets/86ccc31c-daa9-42af-9b18-d51dbad4b0ec)

# now compile the c program using Ofast Command and if you calcluate the number of steps it will be 12
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sumton.o sumton.c

```
now  run the command ibn another terminal
```
riscv64-unknown-elf-objdump -d sumton.o | less
```
![task2 ofast](https://github.com/user-attachments/assets/3a08145d-c5b7-49bd-bb74-75c36e3de6df)
</details>


<details>
<summary>Lab 2</summary>
<br>
  
### objective
1.Debugging the main function using spike simulation and observing the register values
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

</details>

<details>
<summary>Lab 3</summary>
<br>
  
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
-------------------------------------------------------------------------------------------------
</details>

<details>
<summary>Lab 4</summary>
<br>
  
****Compilation of following code using GCC compiler****

SOURCE CODE:
```c

#include <stdio.h>

int main() {
    int peopleInside = 0;
    int choice;

    while (1) {
        printf("\n--- People Counter ---\n");
        printf("1. Person Entered\n");
        printf("2. Person Exited\n");
        printf("3. Check Number of People Inside\n");
        printf("4. Exit Program\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                peopleInside++;
                printf("A person has entered. Total people inside: %d\n", peopleInside);
                break;
            case 2:
                if (peopleInside > 0) {
                    peopleInside--;
                    printf("A person has exited. Total people inside: %d\n", peopleInside);
                } else {
                    printf("No one is inside the room!\n");
                }
                break;
            case 3:
                printf("Number of people inside: %d\n", peopleInside);
                break;
            case 4:
                printf("Exiting the program.\n");
                return 0;
            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    }
```
the following code is compiled with below commands

```
gcc peoplecounter.c
./a.out

```


![gcc out](https://github.com/user-attachments/assets/1d8edeb1-e5af-468e-b7f4-8e232251ca64)

now the same code is compiled with riscv compiler with the following commands



```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i peoplecounter.c
spike pk a.out

```

the following screenshot is attatched with riscv compilation

![riscv](https://github.com/user-attachments/assets/6128b0de-be10-4514-91df-21c3c95b038e)
</details>

<details>
<summary>Lab 5</summary>
<br>
  
## Five staged pipeline riscv core 

  This lab session is about building 5 stage pipeline riscv5 core using tl verilog in makerchip online simulator
  
## Tools and languages used:

  1.Maker chip EDA
  
  2.tl verilog
  
  TL-Verilog, or Transaction-Level Verilog, is an extension of the Verilog HDL (Hardware Description Language) designed to simplify the modeling of complex systems. Here are five key points about TL-Verilog:

1. **High-Level Abstraction**: TL-Verilog provides a higher level of abstraction compared to traditional Verilog. It focuses on the transaction level of design, which is more concerned with the interactions and data exchanges between modules rather than their detailed internal structure. This abstraction helps in modeling complex systems more efficiently.

2. **Enhanced Modeling Capabilities**: TL-Verilog introduces constructs for modeling transactions and communication protocols more naturally. This includes support for transaction-level modeling constructs such as `tlm::tlm_sync_enum` and `tlm::tlm_phase`, which simplify the description of data transfers and communication sequences between modules.

3. **Simplified Verification**: TL-Verilog's abstraction helps in creating more straightforward and intuitive testbenches. By focusing on the high-level interactions and transactions, it becomes easier to write and understand testbenches, which can lead to improved verification productivity and effectiveness.

4. **Integration with SystemC**: TL-Verilog is often used in conjunction with SystemC, another high-level modeling language. SystemC provides a rich set of features for system-level modeling, and TL-Verilog can be integrated with SystemC to leverage its strengths in transaction-level modeling while maintaining compatibility with existing Verilog designs.

5. **Improved Design Productivity**: By using TL-Verilog, designers can achieve faster design and verification cycles. The higher level of abstraction allows for quicker modeling of complex systems and reduces the need for low-level implementation details, which can lead to increased productivity and more efficient development processes.

Overall, TL-Verilog is valuable for managing complex system designs and improving the efficiency of both design and verification processes.

## And gate implementation:
![and gate](https://github.com/user-attachments/assets/a12b575d-6f8b-450a-b1da-b51e3b7c6fc8)

## OR gate implementation:
![orgate](https://github.com/user-attachments/assets/cb375f42-efa0-4214-9cdf-e3244168cb62)

## inverter gate implementation:

![inverter](https://github.com/user-attachments/assets/a4f0c6ab-d970-4171-acb5-9ff33eefb074)

## 2:1 mux implementation:

![2;1 mux](https://github.com/user-attachments/assets/180273c9-3d3d-4b76-825f-8405630e9390)

## 2:1 mux vector implementation:

![mux vector](https://github.com/user-attachments/assets/123f9005-398a-4ca6-a5f0-4b9f701e4561)

##SEQUENTIAL CIRCUIT:

## FIBINACCI SERIES implementation:

![Fabonncci series](https://github.com/user-attachments/assets/372ec569-3021-4201-b4bb-76c33014e74f)

## Counter implementation:

![Sequential counter](https://github.com/user-attachments/assets/77e9177a-f42a-487f-be65-1cc69f7bc31b)

## Sequential Calculator implementation:

![image](https://github.com/user-attachments/assets/26439db6-23b4-4689-9719-8641115fe0b9)

CODE ANd WAVEFROM VISUALIZATION OF SEQUENTIAL CALCULATOR :

![image](https://github.com/user-attachments/assets/1b2699fa-424a-4111-ad19-1856782a5e58)

## PIPELINING:

1. **Definition**: Pipelining is a technique used in computer architecture to improve instruction throughput. It involves breaking down the execution pathway of instructions into discrete stages, so that multiple instructions can be processed simultaneously at different stages of completion.

2. **Stages**: In a typical pipelined CPU, the stages might include Instruction Fetch (IF), Instruction Decode (ID), Execution (EX), Memory Access (MEM), and Write Back (WB). Each stage performs a part of the instruction's execution process.

3. **Throughput Improvement**: By overlapping the execution of instructions, pipelining increases the instruction throughput, meaning that more instructions are completed in a given time period compared to a non-pipelined processor.

4. **Pipeline Hazards**: There are potential issues that can arise in pipelining, such as data hazards (when an instruction depends on the result of a previous instruction), control hazards (related to branching and jumps), and structural hazards (when hardware resources are insufficient to support all concurrent operations).

5. **Stalling and Bypassing**: To handle pipeline hazards, techniques like stalling (inserting delays), data forwarding (bypassing), and branch prediction are used. These methods help manage the potential delays and ensure smooth operation of the pipeline.

Pipelining is fundamental to modern CPU design, enabling higher performance and efficiency in executing instructions.

## Fibonocci Sequence with pipelining:

![image](https://github.com/user-attachments/assets/21592213-8c06-4aa2-b775-c082b5293058)

## Calculator with  pipelining:
  Calculator is implemented with pipeling for increasing throughput.

![image](https://github.com/user-attachments/assets/481ce46d-85da-4de0-99f2-d4026f6eae89)





















