### **WRITING A C PROGRAM FOR SUM OF NUMBERS AND COMPILING THE CODE USING GCC and RISC-V COMPILER AND COMPARING THEIR OUTPUTS**
--------------------------------------------------------------------------------------------------------------------------------
# the following code snippet is compiled using gcc and riscv compiler
## **TASK1: Compile code using GCC compiler**
![image](https://github.com/user-attachments/assets/3d7fa23e-e6fc-4795-88cd-e316d5436d70)
the above picture contains c code for sum of numbers from 1 to n 

the output of the code is shown below:

![task1](https://github.com/user-attachments/assets/5168e01b-4f22-4d77-b84d-5152d69ce47d)

#### **TASK2: Compile code using GCC compiler**
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
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### LAB-2
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
-------------------------------------------------------------------------------------------------------------------------------------------------------------------




  
