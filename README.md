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

<details>
<summary>Lab 6</summary>
<br>
  
# Simulation Workflow: Converting TLV to Verilog with Sandpiper, Creating a Testbench with rvmyth, Running Simulations in Icarus Verilog, and Viewing Results in GTKWave.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# RISC-V Pre-Synthesis Simulation

## Aim

This project aims to demonstrate the comparison of RISC-V pre-synthesis simulation outputs using Icarus Verilog, GTKWave, and Makerchip. The RISC-V processor is designed using TL-Verilog in the Makerchip IDE, converted to Verilog using the Sandpiper-SaaS compiler, and then simulated using Icarus Verilog and GTKWave.

## Prerequisites

Before you begin, ensure you have the following tools and libraries installed:

- **Python 3**
- **Python3-venv**: For creating isolated Python environments
- **pip**: Python package installer
- **Git**: Version control system
- **Icarus Verilog**: Open-source Verilog simulator
- **GTKWave**: Waveform viewer
- **Docker**: For containerization support
- **Sandpiper-SaaS**: TL-Verilog to Verilog compiler

## Installation Instructions

### 1. Install Required Packages

Run the following commands to install necessary packages:

```bash
sudo apt update
sudo apt install -y make python python3 python3-pip git iverilog gtkwave docker.io
sudo chmod 666 /var/run/docker.sock
sudo apt-get install python3-venv
```

### 2. Set Up Python Environment

Create a Python virtual environment and install required Python packages:

```bash
cd ~
python3 -m venv .venv
source ~/.venv/bin/activate
pip install pyyaml click sandpiper-saas
```

### 3. Clone the Repository

Clone the VSDBabySoC repository:

```bash
git clone https://github.com/manili/VSDBabySoC.git
```

### 4. Replace TL-Verilog File

Replace the existing `.tlv` file in the `VSDBabySoC/src/module` directory with your custom RISC-V `.tlv` file. This file should contain your RISC-V processor design.

### 5. Navigate to the Project Directory

Change to the cloned repository directory:

```bash
cd VSDBabySoC
```

### 6. Convert TL-Verilog to Verilog

Use Sandpiper-SaaS to convert your TL-Verilog design to Verilog:

```bash
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```

### 7. Create Pre-Synthesis Simulation File

Generate the pre-synthesis simulation file:

```bash
make pre_synth_sim
```

### 8. Compile and Simulate RISC-V Design

Compile the Verilog files and run the simulation:

```bash
iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
```

### 9. Run the Simulation Output

Execute the simulation to generate the waveform:

```bash
cd output
./pre_synth_sim.out
```

### 10. View Simulation Results with GTKWave

Open the waveform file in GTKWave:

```bash
gtkwave pre_synth_sim.vcd
```

### 11. Analyze the Waveforms

Use GTKWave to analyze and compare the output waveforms to validate the RISC-V processor design.

## GTKWave Output Waveform

- **Clock Signal**
- **Reset Signal**
- **10-bit Output Showing Incremental Values**

## Comparison of Output Waveforms


Review and compare waveform outputs from  Makerchip and GTKwave  to ensure design accuracy.

![image](https://github.com/user-attachments/assets/d8ba7ca9-4864-40f8-a45e-e25a5f9dd238)

![WhatsApp Image 2024-08-27 at 12 58 00 AM](https://github.com/user-attachments/assets/ba352868-64d1-45f8-ab17-e4b5c7a6bb62)


## Conclusion

The waveform outputs from GTKWave and Makerchip match perfectly, validating the accuracy and robustness of the RISC-V processor design.

---
</details>


<details>
<summary>Lab 7</summary>
<br>

## Integration of Peripherals for Digital-to-Analog Conversion Using DAC and PLL 🎛️🔄

In this assignment, we integrate two essential peripherals to convert digital signals to analog output: **Phase-Locked Loop (PLL)** and **Digital-to-Analog Converter (DAC)**.

### **Phase-Locked Loop (PLL) ⏱️🔄**
The onboard crystal oscillator provides a clock frequency between 12-20 MHz. Since our processor operates around 100 MHz, we need to increase this lower frequency. The PLL performs this function by taking the crystal oscillator's clock as input and producing a higher frequency clock for our RISC-V core, labeled as `CPU_clk_GOUR_a0`.

### **Digital-to-Analog Converter (DAC) 🔢➡️🔊**
While our processor deals with digital signals, communication in the real world occurs in analog form. To transform the digital output from the RISC-V core into an analog signal, we use the DAC IP.

### **Commands Used** 🖥️
```bash
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
cd output/
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```
the following screen shots displays the commands and outputs of the assignment

![image](https://github.com/user-attachments/assets/79e0b806-076e-414c-b296-e3870ea11bab)


![Screenshot from 2024-09-02 20-34-46](https://github.com/user-attachments/assets/3a59c5f7-ad72-451f-a77c-30a9afdbf5b1)


</details>

<details>
<summary>Lab 8</summary>
<br>
  
### **RTL Design using Verilog with SKY130 Technology** 🚀✨

<details>
<summary>Day-1</summary>
<br>
  
## Simulation flow based on iverilog

![image](https://github.com/user-attachments/assets/a7df98e7-2e2b-4867-a1f3-380c209385cc)

## LAB-1:
# Aim: Making the setup in local system and cloning the required files from github repository:

# Commands to excute:
```
sudo -i
sudo apt-get install git
ls
cd /home
mkdir VLSI
cd VLSI
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
ls
```

# Terminal Screenshots:

![day1-1](https://github.com/user-attachments/assets/f2de2b44-fe9b-4b2f-a6b1-acf11af41afc)

![day1-2](https://github.com/user-attachments/assets/60efbd1a-a688-40cb-a671-8c24bf1341ae)

![day1-3](https://github.com/user-attachments/assets/50f5ed6e-318d-4ded-83cf-9031650c4d58)


## LAB-2:
# Aim : Working wiht iverilog gtkwave:
We are going to implement 2:1 multiplexer.

## Commands :
```
gvim tb_good_mux.v -o good_mux.v
```
![lab2](https://github.com/user-attachments/assets/215af7fd-3e05-4552-9aaa-3504647ee256)

## Steps to implement the waveform on gtkwave:

```
iverilog good_mux.v tb_good_mux.v
ls
./a.out
gtkwave tb_good_mux.vcd

```
##  Termianl and gtkwaveform screenshots:

```
iverilog good_mux.v tb_good_mux.v
ls
./a.out
gtkwave tb_good_mux.vcd
```

![image](https://github.com/user-attachments/assets/175d3826-1fb2-4549-a13b-d314943ae966)

![lab](https://github.com/user-attachments/assets/1b72ec15-95a5-41a1-948b-600954b0fa45)


## LAB-3:
# Aim : Synthesizing of  2:1 multiplexer using Yosys and Logic Synthesis :

## Yosys :
Yosys is an open-source synthesis tool for digital circuits that supports various hardware description languages, including Verilog. It enables users to transform RTL designs into netlists, making it ideal for FPGA and ASIC design flows. With its extensible architecture, Yosys integrates well with other EDA tools, allowing for a flexible design process.

# YOSYS SETUP:
![image](https://github.com/user-attachments/assets/3e29db19-2920-4a69-b6db-521b5fe516a6)

# Synthesis Verification :
![image](https://github.com/user-attachments/assets/a7bfd470-a955-4858-a383-c0ffda291705)

# Logic synthesis:
Logic synthesis is the process of transforming high-level design descriptions (like RTL) into a gate-level representation. 🏗️ It optimizes the design for performance, area, and power consumption, ensuring it meets specified requirements. ⚡🔍 By automating this process, designers can quickly iterate and refine their circuits for better efficiency! ✨

## Commands :
#  To Start the yosys :
```
yosys
```
![yosys](https://github.com/user-attachments/assets/4222fb74-fea1-41fb-a8e9-90acdb0387e5)


# Load the sky130 standard library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![read](https://github.com/user-attachments/assets/df605b0c-0e8d-4087-bab2-9c21aa77d111)


# Read the design files :
```
read_verilog good_mux.v

```
# Synthesize the top level module :
```
synth -top good_mux
```
![synth](https://github.com/user-attachments/assets/7e90f84b-0bc7-4658-89ae-f9ab40c9ab49)

# Mappping to standard library:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/user-attachments/assets/2abf99b6-57c0-496e-95d7-6788544b7e9a)


![image](https://github.com/user-attachments/assets/f243b4e8-ea3b-4481-b270-5c38e92c664f)

# To observe the graphical representation of generated logic :

```
show
```

![image](https://github.com/user-attachments/assets/b829aa5d-bc4e-490e-a5c7-d409b7616674)

# TO generate netlist and saving it , netlist file will be generated in the current directory
```
write_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v
```

![image](https://github.com/user-attachments/assets/829f52f2-4a3e-4d70-9a07-505029e9818f)


 </details>

<details>
<summary>Day-2</summary>
<br>

## Timing libs, hierarchical vs flat synthesis and efficient flop coding stylesLAB-4:

# LAB-4:
```
sudo -i
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/lib
gvim sky130_fd_sc_hd__tt_025C_1v80.lib
```
![lab4-1](https://github.com/user-attachments/assets/a1d4358f-0ff2-4a38-b62a-4499db58073d)

The .lib file contains essential information about the process technology used, such as 130nm technology, along with process conditions like temperature and voltage. It also outlines various constraints, including variable units and the specific technology type. For instance:

- `technology("cmos")`: Indicates the technology is CMOS.
- `delay_model : "table_lookup"`: Specifies the delay model used.
- `bus_naming_style : "%s[%d]"`: Sets the naming convention for buses.
- `time_unit : "1ns"`: Defines the time unit.
- `voltage_unit : "1V"`: Establishes the voltage unit.
- `leakage_power_unit : "1nW"`: Sets the unit for leakage power.
- `current_unit : "1mA"`: Defines the current unit.
- `pulling_resistance_unit : "1kohm"`: Specifies the unit for pulling resistance.
- `capacitive_load_unit(1.0000000000, "pf")`: Sets the unit for capacitive load.

Additionally, the .lib file details the characteristics of various cells, including leakage power, power consumption, area, input capacitance, and delay for different input combinations.

# Considering a two input AND gate:

![lab4-2](https://github.com/user-attachments/assets/8ebb2d36-646c-4136-981e-1f8a926244fc)

# LAB-5:
Hierarchical vs flat synthesis & Various Flop Coding Styles and optimization:

# Hierarchical Synthesis:
```
cd ~
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
```

![lab5](https://github.com/user-attachments/assets/61c9a60b-1a73-4110-8e50-55526c76da2a)

# To Synthesize the Design:
```
synth -top multiple_modules
```
When we execute the command `synth -top multiple_modules` in Yosys, hierarchical synthesis is carried out. This approach preserves the relationships between the modules, maintaining the module hierarchy throughout the synthesis process.

![lab5-2](https://github.com/user-attachments/assets/5c515d0c-abed-4787-a9fc-33abf46a59f1)

# Multiple Modules: - 2 SubModules
Commands to generate the netlist & Create a Graphical Representation of Logic for Multiple Modules:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
```

![lab5-3](https://github.com/user-attachments/assets/9d463817-a8c3-4279-bac4-793fd4e6bd92)

Commands to write the netlist and view it:
```
write_verilog -noattr multiple_modules_hier.v
!vim multiple_modules_hier.v
```
![lab5-4](https://github.com/user-attachments/assets/bdcd23b5-ec78-4bc7-8cb8-55ac6bfc73c3)

# Flattening: To merge all hierarchical modules in the design into a single module and generate a flat netlist, simply type the following command:

```
flatten

```
# Commands to write the netlist and view it:

```
write_verilog -noattr multiple_modules_hier.v
!vim multiple_modules_hier.v

```
![lab5-5](https://github.com/user-attachments/assets/57468c8f-fc51-4803-a74b-f40934f09255)

![lab5-6](https://github.com/user-attachments/assets/2ad0786d-4e65-4fdb-9bd1-01351476def2)

## Graphical Representation of Logic for Multiple Modules:

```
show
```

![lab5-7](https://github.com/user-attachments/assets/79d91603-e0cc-4c34-abb1-7e7882cef79b)


## D Flip-Flop Design and Simulation Using Icarus Verilog, GTKWave, and Yosys:

This project showcases different coding styles for D Flip-Flops and includes simulations using Icarus Verilog and GTKWave. It also addresses the synthesis of these designs with Yosys. The simulations concentrate on three types of D Flip-Flops:

- D Flip-Flop with Asynchronous Reset
- D Flip-Flop with Asynchronous Set
- D Flip-Flop with Synchronous Reset

  # 1.D Flip-Flop with Asynchronous Reset:
  
  Verilog code for the D Flip-Flop with an asynchronous reset:
  
  ```
  module dff_asyncres(input clk, input async_reset, input d, output reg q);
	always@(posedge clk, posedge async_reset)
	begin
		if(async_reset)
			q <= 1'b0;
		else
			q <= d;
	end
  endmodule

Testbench for Asynchronous Reset D Flip-Flop:
```
module tb_dff_asyncres; 
	reg clk, async_reset, d;
	wire q;
	dff_asyncres uut (.clk(clk), .async_reset(async_reset), .d(d), .q(q));

	initial begin
		$dumpfile("tb_dff_asyncres.vcd");
		$dumpvars(0, tb_dff_asyncres);
		clk = 0;
		async_reset = 1;
		d = 0;
		#3000 $finish;
	end
	
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 async_reset = ~async_reset; 
 endmodule
```
Steps to Run the Simulation:

1. Navigate to the directory where the Verilog files are located:
```
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Run the following commands to compile and simulate the design:

```
iverilog dff_asyncres.v tb_dff_asyncres.v
ls
```

The compiled output will be saved as a.out.

3.Execute the compiled output and open the waveform viewer:
```
./a.out
gtkwave tb_dff_asyncres.vcd
```
By following these steps,we can observe the behavior of the D Flip-Flop with an asynchronous reset in the waveform viewer:

![image](https://github.com/user-attachments/assets/9628e5bc-50cc-4990-b33d-cd36b541d461)

![image](https://github.com/user-attachments/assets/2b3fa89b-da8b-48a8-a916-d2413b845147)


Observation: The waveform shows that when the asynchronous reset is activated (set high), the Q output immediately resets to zero, independent of the clock's positive or negative edge. This illustrates the asynchronous nature of the reset signal.

## 2.D Flip-Flop with Asynchronous Set:

This section illustrates the implementation of a D Flip-Flop with an asynchronous set using Verilog. The design guarantees that when the asynchronous set signal is high, the output Q is immediately set to 1, regardless of the clock signal.

**Verilog Code for Asynchronous Set D Flip-Flop:**

```
module dff_async_set(input clk, input async_set, input d, output reg q);
	always@(posedge clk, posedge async_set)
	begin
		if(async_set)
			q <= 1'b1;
		else
			q <= d;
	end
endmodule
```
Testbench Code:
```
module tb_dff_async_set; 
	reg clk, async_set, d;
	wire q;
	dff_async_set uut (.clk(clk), .async_set(async_set), .d(d), .q(q));

	initial begin
		$dumpfile("tb_dff_async_set.vcd");
		$dumpvars(0, tb_dff_async_set);
		// Initialize Inputs
		clk = 0;
		async_set = 1;
		d = 0;
		#3000 $finish;
	end

	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 async_set = ~async_set; 
endmodule
```
Steps to Run the Simulation:

1.Navigate to the directory containing the Verilog files:
```
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Compile the Verilog code and the testbench using Icarus Verilog:
```
iverilog dff_async_set.v tb_dff_async_set.v
ls
```
The output will be saved as a.out.
3.Run the compiled file and open the waveform in GTKWave:
```
./a.out
gtkwave tb_dff_async_set.vcd
```

![image](https://github.com/user-attachments/assets/7b64d986-e595-406a-a89a-fb093638b9f4)

Observation: The waveform clearly shows that the Q output switches to one when the asynchronous set is asserted high, regardless of the clock edge (positive or negative).

# 3. D Flip-Flop with Synchronous Reset:

This section includes Verilog code to implement a D Flip-Flop with a synchronous reset.

The Verilog code defines a D Flip-Flop that features an active-high synchronous reset. When the reset signal is asserted during a clock edge, the output Q is set to 0. Otherwise, the flip-flop captures the value of D on the rising edge of the clock.
```
module dff_syncres (input clk,
    input sync_reset,
    input d,
    output reg q
);
    
    always @(posedge clk) begin
        if (sync_reset)
            q <= 1'b0;
        else
            q <= d;
    end
endmodule
```
Testbench Code:
```
module tb_dff_syncres;
    reg clk, sync_reset, d;
    wire q;

    // Instantiate the Device Under Test (DUT)
    dff_syncres uut (.clk(clk), .sync_reset(sync_reset), .d(d), .q(q));

    initial begin
        // Initialize waveform dump
        $dumpfile("tb_dff_syncres.vcd");
        $dumpvars(0, tb_dff_syncres);

        // Initialize inputs
        clk = 0;
        sync_reset = 1;
        d = 0;

        // End simulation after a set time
        #3000 $finish;
    end

    // Clock generation
    always #10 clk = ~clk;

    // Toggle the input `d` every 23 time units
    always #23 d = ~d;

    // Toggle the reset signal every 547 time units
    always #547 sync_reset = ~sync_reset;
endmodule
```


Steps to Run the Simulation:
1.Navigate to the directory containing the Verilog files:
```
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Compile the Verilog code and the testbench using Icarus Verilog:

```
iverilog dff_async_set.v tb_dff_async_set.v
ls
``
The output will be saved as a.out.
```
3.Run the compiled file and open the waveform in GTKWave:
```
./a.out
gtkwave tb_dff_async_set.vcd
```
Result: After running the simulation, we will observe the behavior of the D Flip-Flop with an Synchronous Reset in the waveform viewer. Below is a snapshot of the commands and the resulting waveforms.

![image](https://github.com/user-attachments/assets/be4ce50f-ad81-446f-9fae-30887a030230)

Observation: From the waveform, it is evident that the Q output transitions to zero when the synchronous reset is asserted high, but only at the positive edge of the clock signal.

## Synthesis of Various D-Flip-Flops using Yosys

This repository demonstrates the synthesis and simulation of three types of D-Flip-Flops using Yosys:

   
1.Asynchronous Reset
2. Asynchronous Set
3. Synchronous Reset

# 1. Asynchronous Reset D Flip-Flop

1.Navigate to the required directory:
```
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Launch Yosys:

```
yosys
```
3.Read the standard cell library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog design files:
```
read_verilog dff_asyncres.v
```
5.Synthesize the design:
```
synth -top dff_asyncres
```
6. Generate the netlist
```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Create a graphical representation of the Asynchronous Reset D Flip-Flop:
```
show
```

![image](https://github.com/user-attachments/assets/97ce1f00-4a2f-41e5-9f55-12f208636695)

# 2. Asynchronous Set D Flip-Flop

# Command Steps for Synthesis
Follow the steps below to synthesize the asynchronous set D Flip-Flop design:
1.Navigate to the required directory:
```
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Launch Yosys:
```
yosys
```
3.Read the standard cell library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog design files:
```
read_verilog dff_async_set.v
```
5.Synthesize the design:
```
synth -top dff_async_set
```
6.Generate the netlist:
```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Create a graphical representation of the Asynchronous Set D Flip-Flop:
```
show
```
![image](https://github.com/user-attachments/assets/143fa825-5c8d-4b14-b526-531ded510c94)

## 3. Synchronous Reset D Flip-Flop

Command Steps for Synthesis

Follow the steps below to synthesize the synchronous reset D Flip-Flop design:

1.Navigate to the required directory:

```
cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Launch Yosys:
```
yosys
```
3.Read the standard cell library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog design files:
```
read_verilog dff_syncres.v
```
5.Synthesize the design:
```
synth -top dff_syncres
```
6.Generate the netlist:
```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Create a graphical representation of the Synchronous Reset D Flip-Flop:
```
show
```
![image](https://github.com/user-attachments/assets/aa150b2b-b98e-4856-9711-abba658f89c9)

## Multiplication by 2: 
In this tutorial, we learn that specific multiplier hardware is not necessary for multiplying a number by 2. This operation can be easily achieved by concatenating the number with a zero in the least significant bit (LSB). 
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog mult_2.v
4. synth -top mul2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr mul2_net.v
8. gvim mul2_net.v
```

```
//Design
module mul2(input [2:0]a, output [3:0]y);
	assign y=a*2;
endmodule
```
```
//Generated Netlist
module mul2(a,y);
	input [2:0]a; wire [2:0]a;
	output [3:0]y; wire [3:0]y;

	assign y = {a,1'h0};
endmodule
```
![image](https://github.com/user-attachments/assets/996bea2b-ab6b-465d-85c8-22427141c172)
![image](https://github.com/user-attachments/assets/4b0528f5-ae03-434d-b4cf-1e748166881d)

## Multiplication by 8:
In this tutorial, we discover that specific multiplier hardware is not needed for multiplying a number by 8. This operation can be easily accomplished by concatenating the number with itself.

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog mult_9.v
4. synth -top mult9
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr mul9_net.v
8. gvim mul9_net.v
```
```
//Design
module mul2(input [2:0]a, output [5:0]y);
	assign y=a*9;
endmodule
```
```
//Generated Netlist
module mul9(a,y);
	input [2:0]a; wire [2:0]a;
	output [5:0]y; wire [5:0]y;

	assign y = {a,a};
endmodule
```



![image](https://github.com/user-attachments/assets/1c23b162-7765-47a4-9205-3ba64c4b1537)
![image](https://github.com/user-attachments/assets/bc107f39-ab1a-4531-8c16-d518625e9a84)


 </details>
 
<details>
<summary>Day-3</summary>
<br>

## LAB-6:
## Optimization of Various Combinational Designs using Yosys:
This section demonstrates the synthesis and optimization of various combinational designs using Yosys.

## Combinational Designs:

    2-input AND gate
    2-input OR gate
    3-input AND gate
    2-input XNOR gate (3-input Boolean Logic)
    Multiple Module Optimization-1
    Multiple Module Optimization-2
    
## 1. 2-input AND Gate
# Verilog Code:
```
module opt_check(input a, input b, output y);
	assign y = a?b:0;
endmodule
```
# Command Steps for Synthesis:

1. Navigate to the required directory:

   ```
   cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
   ```
2.Launch Yosys:
```
yosys
```
3.Read the standard cell library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog design files:
```
read_verilog opt_check.v
```
5. Synthesize the design:
```
synth -top opt_check
```
![image](https://github.com/user-attachments/assets/ee9291e0-15dd-4d74-a3f4-c921464577a5)

6.Generate the netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Remove unused or redundant logic:
```
opt_clean -purge
```
8. Create a graphical representation:

```
show
```
![image](https://github.com/user-attachments/assets/16e111ef-6a9d-4e04-a3ad-3138ae766d9d)

## 2. 2-input OR Gate

# Verilog Code:
```
module opt_check2(input a, input b, output y);
	assign y = a?1:b;
endmodule
```

Command Steps for Synthesis:

Repeat the same steps as for the 2-input AND gate with the following changes:

1.Use opt_check2.v as the Verilog file:
```
read_verilog opt_check2.v
```
2.Synthesize the design with opt_check2:
```
synth -top opt_check2
```
![image](https://github.com/user-attachments/assets/745ceb2f-34ec-4f25-b98f-4200c776d490)

3.Generate the netlist:

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Remove unused or redundant logic:
```
opt_clean -purge
```
5.Create a graphical representation:
```
show
```
![image](https://github.com/user-attachments/assets/cbeec15a-15a5-4649-a251-d5e57c9dc435)

## 3. 3-input AND Gate

# Verilog Code:
```
module opt_check3(input a, input b, input c, output y);
	assign y = a?(b?c:0):0;
endmodule
```
command Steps for Synthesis:

Follow the same steps as for the 2-input AND gate with the following changes:

1.Use opt_check3.v as the Verilog file:
```
read_verilog opt_check3.v
```
2.Synthesize the design with opt_check3
```
synth -top opt_check3
```
![image](https://github.com/user-attachments/assets/b42ecff3-202f-4442-9eb9-60a718af72fe)

3.Generate the netlist:

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Remove unused or redundant logic:
```
opt_clean -purge
```
5.Create a graphical representation:
```
show
```
![image](https://github.com/user-attachments/assets/54e37518-fbfc-42c0-8d83-4520ed6091e5)

## 4. 2-input XNOR Gate (3-input Boolean Logic)

# Verilog Code:
```
module opt_check4(input a, input b, input c, output y);
	assign y = a ? (b ? ~c : c) : ~c;
endmodule
```
# Steps for Synthesis:

1. Navigate to the required directory:

   ```
   cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
   ```
2.Launch Yosys:
```
yosys
```
3.Read the standard cell library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog design files:
```
read_verilog opt_check4.v
```
5. Synthesize the design:
```
synth -top opt_check4
```
![image](https://github.com/user-attachments/assets/6eea9f58-4659-4e3e-a2a8-64d97ea82d88)

6.Generate the Netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Optimize the Design:
```
opt_clean -purge
```
8.Visualize the Schematic:

```
show
```
![image](https://github.com/user-attachments/assets/6e15d7e9-bfe0-43bf-b14c-6d2c5b42db20)

##  Multiple Module Optimization - 1:

Verilog Code:

The following Verilog code describes a multi-module design using submodules for logic optimization.
```
module sub_module1(input a, input b, output y);
assign y = a & b;
endmodule

module sub_module2(input a, input b, output y);
assign y = a ^ b;
endmodule

module multiple_module_opt(input a, input b, input c, input d, output y);
wire n1, n2, n3;

sub_module1 U1 (.a(a), .b(1'b1), .y(n1));
sub_module2 U2 (.a(n1), .b(1'b0), .y(n2));
sub_module2 U3 (.a(b), .b(d), .y(n3));

assign y = c | (b & n1);
endmodule
```
Steps for Synthesis:
1.Navigate to the Directory:
 ```
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Start the Yosys Tool:
```
yosys
```
3.Read the Library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog File:
```
read_verilog multiple_module_opt.v


```
5. Synthesize the Design:
```
synth -top multiple_module_opt

```
![image](https://github.com/user-attachments/assets/b79eec43-3c93-411a-9187-ef0e9a3b55d7)

6.Generate the Netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Optimize the Design:
```
opt_clean -purge
```
8.Flattening merges hierarchies:
```
flatten
```
9.Visualize the Schematic:
```
show
```
![image](https://github.com/user-attachments/assets/4d2e3a6f-3bee-47dd-a138-884f5b521416)

## Multiple Module Optimization - 2
# Verilog Code:
This is another example of multi-module optimization with a different configuration.
```
module sub_module(input a, input b, output y);
assign y = a & b;
endmodule

module multiple_module_opt2(input a, input b, input c, input d, output y);
wire n1, n2, n3;
sub_module U1 (.a(a), .b(1'b0), .y(n1));
sub_module U2 (.a(b), .b(c), .y(n2));
sub_module U3 (.a(n2), .b(d), .y(n3));
sub_module U4 (.a(n3), .b(n1), .y(y));
endmodule

```
1.Navigate to the Directory:
 ```
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
2.Start the Yosys Tool:
```
yosys
```
3.Read the Library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
4.Read the Verilog File:
```
read_verilog multiple_module_opt2.v


```
5. Synthesize the Design:
```
synth -top multiple_module_opt2

```
![image](https://github.com/user-attachments/assets/0f1b1a30-13bc-47cc-8192-96a8312bfbd7)


6.Generate the Netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
7.Optimize the Design:
```
opt_clean -purge
```
8.Flattening merges hierarchies:
```
flatten
```
9.Visualize the Schematic:
```
show
```
![image](https://github.com/user-attachments/assets/6acfca87-700e-4543-9e8c-7a0d23c0f95a)

## Lab 2: Optimization of Various Sequential Designs

# D-Flipflop Constant 1 with Asynchronous Reset (active low)

This section covers the implementation of a D Flip-Flop featuring an active low asynchronous reset. Below is the corresponding Verilog code:
```
 module dff_const1(input clk, input reset, output reg q);
 always @(posedge clk or posedge reset) begin
     if (reset)
         q <= 1'b0;  // Output is set to 0 when reset is active
     else
         q <= 1'b1;  // Output is set to 1 on the rising edge of the clock
 end
 endmodule
 ```

The testbench designed to simulate the behavior of this D Flip-Flop is as follows:

```verilog
 module tb_dff_const1;
   reg clk, reset;
   wire q;

   dff_const1 uut (.clk(clk), .reset(reset), .q(q));

   initial begin
       $dumpfile("tb_dff_const1.vcd");
       $dumpvars(0, tb_dff_const1);
       // Initialize Inputs
       clk = 0;
       reset = 1;
       #3000 $finish; // End simulation after 3000 time units
   end

   always #10 clk = ~clk; // Generate clock signal with a period of 20 time units
   always #1547 reset = ~reset; // Toggle reset signal periodically
 endmodule
```
Command Steps:

To execute the design and observe the waveform, navigate to the required directory and execute the following commands:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files

```
Use the following commands to compile and simulate the design:
```
 iverilog dff_const1.v tb_dff_const1.v
 ls
```
The iverilog command compiles the design and outputs an executable named a.out. To run this executable and observe the waveform, use:
```
 ./a.out
 gtkwave tb_dff_const1.vcd
```

![image](https://github.com/user-attachments/assets/6e3bcdd5-16f2-40b8-bd32-96f7d2ebe4bc)


Observation: The waveform indicates that the output ( Q ) is high whenever the reset signal is low, showing that the reset operation is independent of the clock edge.

Synthesis:

To synthesize the design, navigate to the required directory again:

```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```

Start Yosys and execute the following commands:
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog dff_const1.v
 synth -top dff_const1
```
![image](https://github.com/user-attachments/assets/731dffbb-d551-4f87-a38c-a2e260ee286b)


Generate the netlist with:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

To create a graphical representation of the synthesized design, use:
```
 show
```
![image](https://github.com/user-attachments/assets/9ac415de-09ad-4c20-95a0-0aee5c63ea5b)


Observation: Since the reset condition does not rely on the clock edge, the D Flip-Flop remains unchanged in the synthesized output.

# 2. D-Flipflop Constant 2 with Asynchronous Reset (active high)

In this section, we explore a D Flip-Flop with an active high asynchronous reset. The Verilog implementation is as follows:
```
 module dff_const2(input clk, input reset, output reg q);
 always @(posedge clk or posedge reset) begin
     if (reset)
         q <= 1'b1;  // Output is set to 1 when reset is active
     else
         q <= 1'b1;  // Output remains 1 on the rising edge of the clock
 end
 endmodule
```
The associated testbench code for this Flip-Flop is:

```
 module tb_dff_const2;
   reg clk, reset;
   wire q;

   dff_const2 uut (.clk(clk), .reset(reset), .q(q));

   initial begin
       $dumpfile("tb_dff_const2.vcd");
       $dumpvars(0, tb_dff_const2);
       // Initialize Inputs
       clk = 0;
       reset = 1;
       #3000 $finish; // Terminate simulation after 3000 time units
   end

   always #10 clk = ~clk; // Generate clock signal
   always #1547 reset = ~reset; // Toggle reset signal
 endmodule
```
Command Steps:

To compile and simulate this design, navigate to the same directory:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files

```
Execute the following commands:
```
 iverilog dff_const2.v tb_dff_const2.v
 ls
```
To run the simulation and view the waveform:
```
 ./a.out
 gtkwave tb_dff_const2.vcd
```
![image](https://github.com/user-attachments/assets/1fd0c768-b6f1-4152-88f9-c09d9fade53e)

Observation: The waveform reveals that the output ( Q ) is consistently high, regardless of the reset signal.

 Synthesis:
 
 For synthesis, navigate to the directory again:
 ```
sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
Start Yosys and run these commands:
```
yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog dff_const2.v
 synth -top dff_const2
```
![image](https://github.com/user-attachments/assets/0ac94f52-04ae-42a6-a355-222bc441d873)

Generate the netlist with:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
To visualize the synthesized design, use:

```
 show
```
![image](https://github.com/user-attachments/assets/83f3ade0-e6f6-4fe8-9aee-1ddec26db72e)

## D-Flipflop Constant 3 with Synchronous Reset (active low)
Here, we examine a D Flip-Flop featuring a synchronous reset that is active low. The Verilog code for this configuration is as follows:
```
 module dff_const3(input clk, input reset, output reg q);
 reg q1;

 always @(posedge clk or posedge reset) begin
     if (reset) begin
         q <= 1'b1;  // Output set to 1 when reset is active
         q1 <= 1'b0; // Intermediate register q1 set to 0
     end else begin	
         q1 <= 1'b1; // Intermediate register q1 set to 1
         q <= q1;    // Output q updates to q1's value
     end
 end
 endmodule
```
The corresponding testbench code is provided below:
```
 module tb_dff_const3;
   reg clk, reset;
   wire q;

   dff_const3 uut (.clk(clk), .reset(reset), .q(q));

   initial begin
       $dumpfile("tb_dff_const3.vcd");
       $dumpvars(0, tb_dff_const3);
       // Initialize Inputs
       clk = 0;
       reset = 1;
       #3000 $finish; // End simulation after 3000 time units
   end

   always #10 clk = ~clk; // Generate clock signal
   always #1547 reset = ~reset; // Toggle reset signal
 endmodule
```
Synthesis:


Again, navigate to the required directory:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
Start Yosys and execute the following commands:
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog dff_const3.v
 synth -top dff_const3
```
![image](https://github.com/user-attachments/assets/a30366b8-4717-4012-84c7-6e73b033056f)
**
Generate the netlist:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
To create a graphical representation of the synthesized design:
```
 show
```
![image](https://github.com/user-attachments/assets/11b87165-4369-4e11-a95c-2936b81482f6)

Observation: This module illustrates that on reset, ( Q ) is set to 1 while ( q1 ) is reset to 0. On each clock cycle, ( q1 ) is updated to 1, and ( Q ) reflects the value of ( q1 ).
##  D-Flipflop Constant 4 with Synchronous Reset (active high):
In this section, we explore a D Flip-Flop with a synchronous reset that is active high. The Verilog code implementation is as follows:
```
 module dff_const4(input clk, input reset, output reg q);
 reg q1;

 always @(posedge clk or posedge reset) begin
     if (reset) begin
         q <= 1'b1;  // Output set to 1 when reset is active
         q1 <= 1'b1; // Intermediate register q1 also set to 1
     end else begin	
         q1 <= 1'b1; // Intermediate register q1 set to 1
         q <= q1;    // Output q updates to the value of q1
     end
 end
 endmodule
```

Synthesis:

To synthesize this design, navigate to the required directory:
```
sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
Launch Yosys and run the following commands:
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog dff_const4.v
 synth -top dff_const4
```

![image](https://github.com/user-attachments/assets/5ebdc607-710a-4b6e-b184-682b52ca1f0d)

Generate the netlist:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Finally, create a graphical representation:
```
 show
```
![image](https://github.com/user-attachments/assets/600c739a-5185-41ea-a383-fd739574b5bc)


Observation: This module specifies that both ( q ) and ( q1 ) are set to 1 upon a positive edge of reset. Consequently, ( Q ) maintains a value of 1, regardless of clock or reset states.

## 5.D-Flipflop Constant 5 with Synchronous Reset:
This section presents a D Flip-Flop with a synchronous reset. The Verilog code is as follows:
```
 module dff_const5(input clk, input reset, output reg q);
 reg q1;

 always @(posedge clk or posedge reset) begin
     if (reset) begin
         q <= 1'b0;  // Output is set to 0 when reset is active
         q1 <= 1'b0; // Intermediate register q1 also reset to 0
     end else begin	
         q1 <= 1'b1; // Intermediate register q1 set to 1
         q <= q1;    // Output q is updated to q1's value
     end
 end
 endmodule
```
# Synthesis:
To synthesize this design, navigate to the required directory:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
Launch Yosys and execute:
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog dff_const5.v
 synth -top dff_const5
```
![image](https://github.com/user-attachments/assets/ec8643ef-2545-482a-af36-571259666f12)


Generate the netlist with:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Create a graphical representation:
```
 show
```
![image](https://github.com/user-attachments/assets/aa0bd4dd-91dd-47fa-9924-dac9db49c064)

Observation: This module defines a D Flip-Flop that resets both ( q ) and ( q1 ) to 0 on a positive edge of reset. On each clock cycle, ( q1 ) is set to 1, and ( q ) is updated accordingly. Therefore, after the first clock cycle following reset, ( Q ) remains 1.
# Counter Optimization 1:
This section covers the implementation of a simple counter optimized for operation. The Verilog code is:
```
 module counter_opt(input clk, input reset, output q);
 reg [2:0] count; // 3-bit counter
 assign q = count[0]; // Output assigned to the least significant bit of count
 
 always @(posedge clk or posedge reset) begin
     if (reset)
         count <= 3'b000; // Reset counter to 0
     else
         count <= count + 1; // Increment counter on clock edge
 end
 endmodule
```
Synthesis:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
Launch Yosys and run:
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog counter_opt.v
 synth -top counter_opt
```
![image](https://github.com/user-attachments/assets/b3cbd38e-4975-4fe0-9ce3-3a4492109535)

Generate the netlist with:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Create a graphical representation:
```
 show
```
![image](https://github.com/user-attachments/assets/9a95bfe4-c243-4866-8165-2dccc416218d)

## 7. Counter Optimization 2:
This section presents an optimized counter design. The Verilog code is as follows:
```
 module counter_opt2(input clk, input reset, output q);
 reg [2:0] count; // 3-bit counter
 assign q = (count[2:0] == 3'b100); // Output set high when count reaches 4
 
 always @(posedge clk or posedge reset) begin
     if (reset)
         count <= 3'b000; // Reset counter to 0
     else
         count <= count + 1; // Increment counter on clock edge
 end
 endmodule
```
Synthesis:
To synthesize this design, navigate to the required directory:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
Launch Yosys and execute:
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog counter_opt2.v
 synth -top counter_opt
```
![image](https://github.com/user-attachments/assets/658a6a59-c996-41b9-a7c6-7eba5a6d78b6)

Generate the netlist with:
```
 dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Finally, create a graphical representation:
```
 show
```
![image](https://github.com/user-attachments/assets/6be0272f-8459-4f13-8368-f5e89b53e935)

</details>
 
<details>
<summary>Day-4</summary>
<br>

## AIM: Gate Level Simulation (GLS), Synthesis-Simulation Mismatch, Non-blocking and Blocking Statements
Gate Level Simulation (GLS) is a crucial step in the digital design verification process. It acts as an important checkpoint where designers verify the accuracy and functionality of the synthesized netlist, which offers a more detailed view of the design compared to the original high-level abstraction. During GLS, simulations are conducted using a testbench to evaluate both the logical correctness and timing performance of the circuit. By analyzing output waveforms and comparing them to expected results, designers can confirm that the synthesis process hasn’t unintentionally introduced errors that could compromise the overall functionality of the design. This stage is particularly important as it provides insights into how well the design meets the required specifications and performance criteria before progressing to physical implementation.

A critical aspect of GLS is the consideration of sensitivity lists in the design. These lists are vital for ensuring the circuit behaves correctly under all conditions. An incomplete sensitivity list can lead to unintended latches, resulting in mismatches between synthesis and simulation. Additionally, understanding the distinction between blocking and non-blocking assignments is essential in this context. Blocking assignments, which execute in sequence, can create situations where the output fails to respond to input changes as expected, potentially leading to errors in simulated behavior. In contrast, non-blocking assignments enable concurrent execution, helping to avoid such issues. Therefore, a thorough analysis of the circuit's behavior, alongside a solid understanding of sensitivity lists and assignment types, is necessary to achieve accurate results in GLS.
## GLS Simulation
# Example 1: 2 x 1 Multiplexer Using Ternary Operator

# Verilog Code:
```
module ternary_operator_mux (input i0, input i1, input sel, output y);
    assign y = sel ? i1 : i0;
endmodule
```
# Command Steps for Simulation:
```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
![image](https://github.com/user-attachments/assets/ef35a196-11d5-4cd4-b02d-899b539364dd)

Synthesis:

This will invoke/start Yosys.
```
yosys
```
Read the Library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Read the Design Verilog Files:
```
read_verilog ternary_operator_mux.v
```
Synthesize the Design:
```
synth -top ternary_operator_mux
```
![image](https://github.com/user-attachments/assets/3e00c28b-e728-48d7-b950-6396405df9c3)

Generate the Netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Create a Graphical Representation:
```
show
```
![image](https://github.com/user-attachments/assets/a9755a97-a08a-41ab-841e-1e138cd9d4a7)

To See the Netlist:
```
write_verilog -noattr ternary_operator_mux_net.v
!gvim ternary_operator_mux_net.v
```
![image](https://github.com/user-attachments/assets/b8c87abc-1325-4468-aad3-78c0bed84167)


# Gate Level Synthesis (GLS):

# Command Steps:
Go to the required directory:

```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
We just need to put a few commands as stated below in order to see the waveforms.
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
ls
```
After giving the above command the IVerilog stores the output as ' a.out '

Now let's execute the ' a.out ' file and observe the waveforms.
```
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
Below is the Snapshot of the above commands and the resultant Waveforms: 

![image](https://github.com/user-attachments/assets/e302e36d-ed15-4e37-ba19-ac32fe66a246)



These waveforms correspond to the GATE LEVEL SYNTHESIS for the Ternary Operator MUX.

## Example 2: Design of a 2:1 Bad MUX

Verilog Code:
```
module bad_mux(input i0, input i1, input sel, output reg y);
	always@(sel)
	begin
		if(sel)
			y <= i1;
		else
			y <= i0;
	end
endmodule
```
Command Steps for Simulation:
```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![image](https://github.com/user-attachments/assets/299fb9e9-5bb1-44c5-8fe3-0c090bd92d5d)

From the waveform, it can be observed that the output y changes only when there is a change in the select line, completely ignoring the change in i0 and i1, which should also change the output y. Thus, this design is that of a bad MUX.
Synthesis:
This will invoke/start Yosys.
```
yosys
```
Read the Library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Read the Design Verilog Files:
```
read_verilog bad_mux.v
```
Synthesize the Design:
```
synth -top bad_mux
```

![image](https://github.com/user-attachments/assets/cc04bf18-144a-430b-885b-f17cf91241d2)

Generate the Netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Create a Graphical Representation:
```
show
```

![image](https://github.com/user-attachments/assets/ca023a8d-f5cc-4521-a89a-73d5e60df468)

To See the Netlist:
```
write_verilog -noattr bad_mux_net.v
!gvim bad_mux_net.v
```

![image](https://github.com/user-attachments/assets/01151d40-092c-4771-961a-0952b045e3de)


From the waveform, it can be observed that the output y changes only when there is a change in the select line, completely ignoring the change in i0 and i1, which should also change the output y. Thus, this design is that of a bad MUX.

## Gate Level Synthesis (GLS)
Command Steps:

Go to the required directory:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
We just need to put a few commands as stated below in order to see the waveforms.
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux.v tb_bad_mux.v
ls

```
After giving the above command, the IVerilog stores the output as ' a.out '

Now let's execute the ' a.out ' file and observe the waveforms.
```
./a.out
gtkwave tb_bad_mux.vcd
```
![image](https://github.com/user-attachments/assets/1ed4ad37-9c8e-4e0b-bb88-c3c9e7413fff)

# Example 3: Blocking Caveat
Verilog Code:
```
module blocking_caveat(input a, input b, input c, output reg d);
	reg x;

	always@(*)
	begin
		d = x & c;
		x = a | b;
	end
endmodule
```
Command Steps for Simulation:
```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
![image](https://github.com/user-attachments/assets/663da905-f600-498e-b3ba-d57e7779aeb7)

As depicted, when A and B go zero, the OR gate output should be zero (X equal to zero), and the AND gate output should also be zero (same as D output). But, the AND gate input of X takes the previous value of A|B equal to one, based on the design created by the blocking statement, hence the discrepancy in the output.

# Synthesis:
This will invoke/start Yosys.
```
yosys
```
Read the Library:
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
synth -top blocking_caveat
```
synth -top blocking_caveat
```
![image](https://github.com/user-attachments/assets/4bbf363c-370c-4ee5-a79a-ee86c8b89f3a)

Generate the Netlist:
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

```
Create a Graphical Representation:
```
show
```
To See the Netlist:
```
write_verilog -noattr blocking_caveat_net.v
!gvim blocking_caveat_net.v
```
![image](https://github.com/user-attachments/assets/5fd53d37-f911-4fc3-9228-46007ed9fcae)

Gate Level Synthesis (GLS)
Command Steps:
Go to the required directory:
```
 sudo -i
 cd ~
 cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
We just need to put a few commands as stated below in order to see the waveforms.
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
ls
```
After giving the above command, the IVerilog stores the output as ' a.out '

Now let's execute the ' a.out ' file and observe the waveforms.
```
./a.out
gtkwave tb_blocking_caveat.vcd
```
Below is the Snapshot of the above commands and the resultant Waveforms: 
![image](https://github.com/user-attachments/assets/f7aef441-cc97-4d1b-99c0-42cbd2dad54a)

These waveforms correspond to the GATE LEVEL SYNTHESIS for the Blocking Caveat.
</details>

</details>
<details>
<summary>Lab 9</summary>
<br>
	
### TASK 11: Synthesize RISC-V and Compare Output with Functional Simulations
# Objective: The objective of this task is to synthesize the RISC-V design and then compare the results with functional simulations.
Steps:
1.Copy the source folder:
Start by copying the `src` folder from the `VSDBabySoC` directory into the `vlsi` folder. After that, transfer it into the `sky130RTLDesignAndSynthesisWorkshop` directory using the following commands:
```
   sudo -i  
   cd /home/arun/vlsi/  
   cp -r src sky130RTLDesignAndSynthesisWorkshop/
```
2.Navigate to the required directory:
Move to the target directory where synthesis will take place:
```
   cd ~  
   cd /home/arun/vlsi/sky130RTLDesignAndSynthesisWorkshop/src/module
```
3.Synthesis:
Start Yosys for synthesis:
Invoke Yosys by entering the following command:
```
  yosys
```
4.Read the library:
Load the standard cell library required for synthesis:
```
   read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
5.Read the Verilog design files:
Import the required Verilog files for clock gating and RISC-V designs:
```
   read_verilog clk_gate.v  
   read_verilog rvmyth.v
```
6.Synthesize the design:
Synthesize the top-level module rvmyth:
```
   synth -top rvmyth
```
![lab91](https://github.com/user-attachments/assets/f3685cdb-582f-497a-ad27-139cf424b9c4)

![lab922](https://github.com/user-attachments/assets/89331441-ef1f-44dc-ae55-d34e0afd898a)

![netlist](https://github.com/user-attachments/assets/9a34d2af-cba9-4869-b29c-5162b2ff4d78)


7. Generate the netlist:
After synthesis, generate the netlist and inspect it:
```
   abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
   write_verilog -noattr rvmyth.v  
   !gvim rvmyth.v  
   exit
```
![lab93](https://github.com/user-attachments/assets/d2c6d388-7318-4a68-9338-0cfaec6a0d4c)

8.Simulate the Synthesized Design:
Observe the synthesized RISC-V output waveform:
Use the following commands to run the simulation and view the waveforms:
```
   iverilog ../../my_lib/verilog_model/primitives.v ../../my_lib/verilog_model/sky130_fd_sc_hd.v rvmyth.v testbench.v vsdbabysoc.v avsddac.v avsdpll.v clk_gate.v  
   ls  
   ./a.out  
   gtkwave dump.vcd
```
Functional Simulations:
Simulate functional design:
Navigate to the VSDBabySoC directory and simulate the pre-synthesized version of the design:
```
   cd ~  
   cd VSDBabySoC  
   iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/  
   ./pre_synth_sim.out  
   gtkwave pre_synth_sim.vcd
```
Comparison:
Comparison of Functionality vs Synthesized Output:
Finally, compare the waveforms of the functional and synthesized simulations to verify correctness.
### o1	
![lab95](https://github.com/user-attachments/assets/af9036f7-8f0f-4f01-b244-0d17dcb9d00f)
## o2
![lab94o2](https://github.com/user-attachments/assets/ea1dd1c6-dcc0-4029-b4bc-51ea2eb70221)

we can see that O1 = O2 so functionality is equal to synthesized Output.

</details>


<details>
<summary>Lab 10</summary>
<br>
	
## TASK : Static Timing Analysis for a Synthesized RISC-V Core with OpenSTA 
# Commands to install tools
Download CUDD from this **[link](https://github.com/davidkebo/cudd/blob/main/cudd_versions/cudd-3.0.0.tar.gz)** and then transfer the downloaded file to your home directory.
```
cd
tar xvfz cudd-3.0.0.tar.gz
cd cudd-3.0.0
./configure
make
```
openSTA
```
cd
sudo apt-get install cmake clang gcc tcl swig bison flex

git clone https://github.com/parallaxsw/OpenSTA.git
cd OpenSTA
cmake -DCUDD_DIR=/home/arun/cudd-3.0.0
make
app/sta
```

![screenshot1](https://github.com/user-attachments/assets/9a95c861-ef35-47db-9e19-3cc0d9e538af)

```
cd /home/arun/OpenSTA
mkdir lab10
```
Download all the required files to directory lab10
# Steps to do Timing Analysis

    Clock period = 9.75ns
    Setup uncertainty and clock transition will be 5% of clock
    Hold uncertainty and data transition will be 8% of clock.

```
cd /home/arun/OpenSTA/app
./sta

read_liberty /home/arun/OpenSTA/lab10/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog /home/arun/OpenSTA/lab10/likith_riscv_netlist.v
link_design rvmyth

create_clock -name clk -period 9.75 [get_ports clk]
set_clock_uncertainty [expr 0.05 * 9.75] -setup [get_clocks clk]
set_clock_uncertainty [expr 0.08 * 9.75] -hold 
[get_clocks clk]
set_clock_transition [expr 0.05 * 9.75] [get_clocks clk]
set_input_transition [expr 0.08 * 9.75] [all_inputs]

report_checks -path_delay max
report_checks -path_delay min
```
To execute the OpenSTA and obtain the timing reports, run the below command,
```
sta scripts/sta.conf
```
Following are contents of the sta.conf file,
```
read_liberty -min ./lib/sta/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max ./lib/sta/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -min ./lib/avsdpll.lib
read_liberty -max ./lib/avsdpll.lib
read_liberty -min ./lib/avsddac.lib
read_liberty -max ./lib/avsddac.lib
read_verilog ./src/module/vsdbabysoc_synth.v
link_design vsdbabysoc
read_sdc ./src/sdc/sta_post_synth.sdc
```


![image](https://github.com/user-attachments/assets/a616f45e-e472-4cdf-b281-5db3fd75f9b9)

![image](https://github.com/user-attachments/assets/bbf2483f-573e-4ddf-be35-32a15bd97b98)


</details>
