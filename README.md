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

the following screenshot contains compilation of c code using gcc compiler

The GCC (GNU Compiler Collection) is an open-source compiler system that supports multiple programming languages, including C, C++, and Fortran. It is widely used for its robust performance and adherence to language standards, making it a popular choice for both academic and commercial software development.

![gcc out](https://github.com/user-attachments/assets/1d8edeb1-e5af-468e-b7f4-8e232251ca64)

now the same code is compiled with riscv compiler with the following commands



```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i peoplecounter.c
spike pk a.out

```

the following screenshot is attatched with riscv compilation

now the code is compiled with riscv compiler to be oompatible with risc v processor core

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

## VALIDITY :
In TL-Verilog, validity is an additional verification step implemented alongside pipelining. It simplifies debugging and enhances error checking, leading to cleaner, more readable code.
## Distance Accumulator with Pythagoras Theorem

Below is the example of distance accumumlator with pythagoras theorem.

Circuit Diagram:

![image](https://github.com/user-attachments/assets/f8adf5a7-2171-4fc5-8451-8c37de61aa77)

Implemented in tl verilog:

![image](https://github.com/user-attachments/assets/5adf25aa-cc75-483a-927e-f0801b5963b7)

## Cycle calculator with validity:

calculator example using validity.

![image](https://github.com/user-attachments/assets/8f18aee7-77a1-4aef-96a7-ef8f04ea5b42)

## Basic RISCV CPU Micro Architecture

The block diagram of the RISCV Micro Architecutre is as shown below.

![image](https://github.com/user-attachments/assets/24d06466-38e1-44e0-8afa-af5c73c64e67)

## Instruction Fetch

Instruction fetch is the process in a CPU where the next instruction to be executed is retrieved from memory into the instruction register.

![image](https://github.com/user-attachments/assets/56c037d0-f369-4889-b4a0-b1b7016b3ab8)

## Instruction Decode

Instruction decode is the CPU process where the binary instruction retrieved from memory is interpreted to identify the operation to execute and the operands required.

![image](https://github.com/user-attachments/assets/3c47d674-e714-4e58-9ab8-58b4a8c31c87)


## Diagram 

![image](https://github.com/user-attachments/assets/31dadc27-3646-49cc-90f1-34daef6b7cd9)

## Register File Read

  Register read is the process in a CPU where data is retrieved from specified registers for use in an instruction's execution.


  ![image](https://github.com/user-attachments/assets/3432f9c6-fdd1-42ab-8559-f7081a41d752)

## Regsiter File Write

   Register write is the process in a CPU where the result of an instruction is stored back into a specified register.

   ![image](https://github.com/user-attachments/assets/25819510-408d-4c11-bf11-ef93afcb3740)


## Complete Pipeline RISC-V CPU Micro Architecture

Here’s an overview of the code's functionality:

- **RISC-V Processor Implementation**: The code constructs a fundamental RISC-V processor in TL-Verilog, managing the processes of instruction fetching, decoding, and execution.

- **Instruction Decoding and Execution**: It interprets instructions to determine their type (e.g., R-type, I-type) and performs the specified operations, such as arithmetic or branching.

- **Register File Management**: The processor handles reading from and writing to registers, efficiently managing the source and destination registers for each instruction.

- **Pipeline Stages**: Pipeline stages are defined using `@`, with each stage dedicated to a specific part of instruction processing, including fetch, decode, and execute stages.

- **Simulation Control**: The code incorporates logic to conclude the simulation after a predetermined number of cycles and to verify whether the results are correct or not.

code:
```
\m4_TLV_version 1d: tl-x.org
\SV
   // Template code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store r10 result in dmem
   m4_asm(LW, r17, r0, 10000)           // Load contents of dmem to r17
   m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_Arun = *clk;
         
         //PC fetch - branch, jumps and loads introduce 2 cycle bubbles in this pipeline
         $pc[31:0] = >>1$reset ? '0 : (>>3$valid_taken_br ? >>3$br_tgt_pc :
                                       >>3$valid_load     ? >>3$inc_pc[31:0] :
                                       >>3$jal_valid      ? >>3$br_tgt_pc :
                                       >>3$jalr_valid     ? >>3$jalr_tgt_pc :
                                                     (>>1$inc_pc[31:0]));
         // Access instruction memory using PC
         $imem_rd_en = ~ $reset;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
         
      @1
         $clock_Arun = *clk;
         //Getting instruction from IMem
         $instr[31:0] = $imem_rd_data[31:0];
         
         //Increment PC
         $inc_pc[31:0] = $pc[31:0] + 32'h4;
         
         //Decoding I,R,S,U,B,J type of instructions based on opcode [6:0]
         //Only [6:2] is used here because this implementation is for RV64I which does not use [1:0]
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         
         $is_r_instr = $instr[6:2] == 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] == 5'b10100;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_b_instr = $instr[6:2] == 5'b11000;
         
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         //Immediate value decode
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20]} :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7]} :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31] , $instr[30:12] , { 12{1'b0}} } :
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} :
                      >>1$imm[31:0];
         
         //Generate valid signals for each instruction fields
         $rs1_or_funct3_valid    = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid              = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid               = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct7_valid           = $is_r_instr;
         
         //Decode other fields of instruction - source and destination registers, funct, opcode
         ?$rs1_or_funct3_valid
            $rs1[4:0]    = $instr[19:15];
            $funct3[2:0] = $instr[14:12];
         
         ?$rs2_valid
            $rs2[4:0]    = $instr[24:20];
         
         ?$rd_valid
            $rd[4:0]     = $instr[11:7];
         
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         
         $opcode[6:0] = $instr[6:0];
         
         //Decode instruction in subset of base instruction set based on RISC-V 32I
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         //Branch instructions
         $is_beq   = $dec_bits ==? 11'bx_000_1100011;
         $is_bne   = $dec_bits ==? 11'bx_001_1100011;
         $is_blt   = $dec_bits ==? 11'bx_100_1100011;
         $is_bge   = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu  = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu  = $dec_bits ==? 11'bx_111_1100011;
         
         //Jump instructions
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal   = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr  = $dec_bits ==? 11'bx_000_1100111;
         
         //Arithmetic instructions
         $is_addi  = $dec_bits ==? 11'bx_000_0010011;
         $is_add   = $dec_bits ==  11'b0_000_0110011;
         $is_lui   = $dec_bits ==? 11'bx_xxx_0110111;
         $is_slti  = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_xori  = $dec_bits ==? 11'bx_100_0010011;
         $is_ori   = $dec_bits ==? 11'bx_110_0010011;
         $is_andi  = $dec_bits ==? 11'bx_111_0010011;
         $is_slli  = $dec_bits ==? 11'b0_001_0010011;
         $is_srli  = $dec_bits ==? 11'b0_101_0010011;
         $is_srai  = $dec_bits ==? 11'b1_101_0010011;
         $is_sub   = $dec_bits ==? 11'b1_000_0110011;
         $is_sll   = $dec_bits ==? 11'b0_001_0110011;
         $is_slt   = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu  = $dec_bits ==? 11'b0_011_0110011;
         $is_xor   = $dec_bits ==? 11'b0_100_0110011;
         $is_srl   = $dec_bits ==? 11'b0_101_0110011;
         $is_sra   = $dec_bits ==? 11'b1_101_0110011;
         $is_or    = $dec_bits ==? 11'b0_110_0110011;
         $is_and   = $dec_bits ==? 11'b0_111_0110011;
         
         //Store instructions
         $is_sb    = $dec_bits ==? 11'bx_000_0100011;
         $is_sh    = $dec_bits ==? 11'bx_001_0100011;
         $is_sw    = $dec_bits ==? 11'bx_010_0100011;
         
         //Load instructions - support only 4 byte load
         $is_load  = $dec_bits ==? 11'bx_xxx_0000011;
         
         $is_jump = $is_jal || $is_jalr;
         
      @2
         //Get Source register values from reg file
         $clock_Arun = *clk;
         $rf_rd_en1 = $rs1_or_funct3_valid;
         $rf_rd_en2 = $rs2_valid;
         
         $rf_rd_index1[4:0] = $rs1[4:0];
         $rf_rd_index2[4:0] = $rs2[4:0];
         
         //Register file bypass logic - data forwarding from ALU to resolve RAW dependence
         $src1_value[31:0] = $rs1_bypass ? >>1$result[31:0] : $rf_rd_data1[31:0];
         $src2_value[31:0] = $rs2_bypass ? >>1$result[31:0] : $rf_rd_data2[31:0];
         
         //Branch target PC computation for branches and JAL
         $br_tgt_pc[31:0] = $imm[31:0] + $pc[31:0];
         
         //RAW dependence check for ALU data forwarding
         //If previous instruction was writing to reg file, and current instruction is reading from same register
         $rs1_bypass = >>1$rf_wr_en && (>>1$rd == $rs1);
         $rs2_bypass = >>1$rf_wr_en && (>>1$rd == $rs2);
         
      @3
         //ALU
         $clock_Arun = *clk;
         $result[31:0] = $is_addi  ? $src1_value +  $imm :
                         $is_add   ? $src1_value +  $src2_value :
                         $is_andi  ? $src1_value &  $imm :
                         $is_ori   ? $src1_value |  $imm :
                         $is_xori  ? $src1_value ^  $imm :
                         $is_slli  ? $src1_value << $imm[5:0]:
                         $is_srli  ? $src1_value >> $imm[5:0]:
                         $is_and   ? $src1_value &  $src2_value:
                         $is_or    ? $src1_value |  $src2_value:
                         $is_xor   ? $src1_value ^  $src2_value:
                         $is_sub   ? $src1_value -  $src2_value:
                         $is_sll   ? $src1_value << $src2_value:
                         $is_srl   ? $src1_value >> $src2_value:
                         $is_sltu  ? $sltu_rslt[31:0]:
                         $is_sltiu ? $sltiu_rslt[31:0]:
                         $is_lui   ? {$imm[31:12], 12'b0}:
                         $is_auipc ? $pc + $imm:
                         $is_jal   ? $pc + 4:
                         $is_jalr  ? $pc + 4:
                         $is_srai  ? ({ {32{$src1_value[31]}} , $src1_value} >> $imm[4:0]) :
                         $is_slt   ? (($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]}):
                         $is_slti  ? (($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]}) :
                         $is_sra   ? ({ {32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $is_load  ? $src1_value +  $imm :
                         $is_s_instr ? $src1_value + $imm :
                                    32'bx;
         
         $sltu_rslt[31:0]  = $src1_value <  $src2_value;
         $sltiu_rslt[31:0] = $src1_value <  $imm;
         
         //Jump instruction target PC computation
         $jalr_tgt_pc[31:0] = $imm[31:0] + $src1_value[31:0]; 
         
         //Branch resolution
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) :
                     1'b0;
         
         //Current instruction is valid if one of the previous 2 instructions were not (taken_branch or load or jump)
         $valid = ~(>>1$valid_taken_br || >>2$valid_taken_br || >>1$is_load || >>2$is_load || >>2$jump_valid || >>1$jump_valid);
         
         //Current instruction is valid & is a taken branch
         $valid_taken_br = $valid && $taken_br;
         
         //Current instruction is valid & is a load
         $valid_load = $valid && $is_load;
         
         //Current instruction is valid & is jump
         $jump_valid = $valid && $is_jump;
         $jal_valid  = $valid && $is_jal;
         $jalr_valid = $valid && $is_jalr;
         
         //Destination register update - ALU result or load result depending on instruction
         $rf_wr_en = (($rd != '0) && $rd_valid && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = $valid ? $rd[4:0] : >>2$rd[4:0];
         $rf_wr_data[31:0] = $valid ? $result[31:0] : >>2$ld_data[31:0];
         
      @4
         //Data memory access for load, store
         $clock_Arun = *clk;
         $dmem_addr[3:0]     =  $result[5:2];
         $dmem_wr_en         =  $valid && $is_s_instr;
         $dmem_wr_data[31:0] =  $src2_value[31:0];
         $dmem_rd_en         =  $valid_load;
         
      
         //Write back data read from load instruction to register
         $ld_data[31:0]      =  $dmem_rd_data[31:0];
         
      
      

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //Checks if sum of numbers from 1 to 9 is obtained in reg[17] and runs 10 cycles extra after this is met
   *passed = |cpu/xreg[17]>>10$value == (1+2+3+4+5+6+7+8+9);
   //Run for 200 cycles without any checks
   //*passed = *cyc_cnt > 200;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```
the diagram visualization of code 

![image](https://github.com/user-attachments/assets/a3aff323-e559-4996-9f41-b85697963a2d)

the viz for the above code

![image](https://github.com/user-attachments/assets/0af94e7c-1fe8-4fab-852d-43efbea699b9)

the following image contains waveforn:

![image](https://github.com/user-attachments/assets/5ad896be-687f-47b4-95f4-4e724898606b)


the following waveform contains the values of reg14:

![image](https://github.com/user-attachments/assets/d8ba7ca9-4864-40f8-a45e-e25a5f9dd238)


</details>



























