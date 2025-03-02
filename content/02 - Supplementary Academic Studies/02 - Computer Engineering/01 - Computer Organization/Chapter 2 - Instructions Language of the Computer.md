# 2.1 - Introduction

- **Instruction set**: The vocabulary of commands understood by a given architecture
-  We can notice that instruction sets for different architectures are more or less the same given that they have the same goal to minimize the power and increase the performance of a system
- **Stored Program Concept**: The idea that instructions and data of many types can be stored in memory as numbers and thus be easy to change, leading to the stored-program computer 
![[RISC-V Instruction Set.png]]
# 2.2 - Operations of the Computer

## Hardware

All computers must be able to perform arithmetic. The RISC-V assembly langauage notation :
``` assembly
add a,b,c
```
 Tells the computer to add the two variables $b$ and $c$ and put the sum into $a$

 It is important to note that the RISC-V arithmetic instruction performs only one operation at a time with exactly 3 variables. That is to say if we wanted to add $b,c,d,e$ into $a$ it would look like
 ```assembly
 add a,b,c // sum of b and c is placed in a
 add a,a,d // sum of b,c, and d is now in a
 add a,a,e // sum of all now in a
```
Which means each line can only contain at most 1 instruction
Though lets say for a higher level language we have the function 
```c++
f = (g+h) - (i+j);
```
This segment of code will look like this for RISC-V
```assembly
add t0,g,h //temporary variable contains g + h
add t1, i, j // temporary variable t1 holds i+i
sub f, t0, t1
```

# 2.3 - Operands of the Computer Hardware

**doubleword**: unit of access in a computer usually a group of 64 bits corresponding to the size of a register in RISC-V architecture
**word**: A unit of access in a computer usually a group of 32 bits

Example : Compiling a C assignment using registers:
It is the compilers job to associate program variables with registers for instance the assignments for the function 
```c
f = (g + h) - (i + j);
```
The variables `f,g,h,i,j` are assigned to the registers `x19,x20,x21,x22,x23` respectively so the output would look like:
```assembly
add x5, x20, x21
add x6, x22, x23
sub x19, x5, x6
```

## Memory Operands

- Data structures and larger data elements are kept in memory. Given that the CPU can only hold a small number of registers 
	- CPUs commonly have between 16-32 registers on them 
- Given this RISC-V include instructions that transfer data between memory and registers this is called **data transfer instructions**
- To access a word or doubleword in memory the instruction must supply the memory **address** , which is a value used to delineate the location of a specific data element within a memory array
- The data transfer instruction that copies data from memory to a register is called **load**

EX: Compiling an assignment when an operand is in memory:
- Assume `A` is an array of 100 doublewords and that the compiler associates the variables `g,h` with `x20,x21`.  Also assume that the arrays starting address (**Base address**) is in `x22`.  then this C compilation assigment for this function would look like :
```C
g = h + A[8];
```
- First we place the data in a temporary register for use in the next instruction:
```assembly
ld x9, 8(x22) // Temp reg x9 gets A[8]
add x20, x21, x9 // g = h + A[8]
```
- Here the `8(x22)` the (8) is called the **offset**

In many architectures, words must start at addresses that are multiples of 4 and doublewords must start at addresses that are multiples of 8. This requirement is called an **alignment restriction**.

Example: Compiling using load and store:
- Assume we have a variable `h` which is at register `x21` and the base address of the array `A` is `x22` :
```c
A[12] = h + A[8];
```
- The following instructions will look like this:
```
ld x9, 64(x22) //Temp reg x9 gets A[8]
add x9, x21, x9 // temp reg x9 gets h + A[8]
sdx9, 96(x22) // Stores h+A[8] back into A[12]
```
- So using 96 ($8 \times 12$) as the offset and register `x22` as the base register
- We also use the first 64 as ($8 \times 8$). Since the register is broken up into 8 bits so if we wanted to access which ever register location we would do ($loc \times 8$)

Commonly programs have more variables than registers so the compiler tries to keep the most frequently used variables in registers and less frequently used variables in memory this is called **spilling** registers. 

Thus, registers take less time to access and have higher throughput than memory, making data in registers both considerably faster to access and simpler to use. Accessing registers also uses much less energy than accessing memory.

## Constant or Immediate Operands

Commonly a program will use a constant in an operation initally this would look like this in instruction sets:
```assembly
ld x9, AddrConstant4(x3) //x9 = constant 4
add x22, x22, x9 // x22 = x22 + x9
```

Though alternatively we can avoid loading an instruction by using a constant operand called **add immediate** or `addi` to add a constant to a register such as:
```assembly
addi x22, x22, 4 //x22 = x22 + 4
```

Adding constants occurs frequently so the `addi` instruction is one of the most used instructions in RISC-V

*Skipped 2.4 its just binary numbers*

# 2.5 Representing Instructions in the Computer

Example: Translating a RISC-V Assembly instruction into a Machine instruction:
- We will start with the instruction:
```
add x9, x20, x21
```
- The decimal representation of this will look like:
	- $0,21,20,0,9,51$
- Here each segment of the instruction is called a **field**
- The 1st,4th and 6th ($0,0,51$) fields correspond to tell the computer that this is an addition operation. 
- The 2nd field gives the number of the register that is the second source operand of the addition operation (21 for `x21)
- The 3rd field gives the other source operand for the addition (21 for `x20`)
- The 5th field contains the number of the register that is to receive the sum (9 for `x9`)
- As binary this would look like (machine language)![[Binaryinstruction.png]]

This layout of instructions is called the **instruction format**

As we can see the RISC-V instructions take exactly 32 bits (a word) or half a doubleword

**Machine Language**: The binary representation used for communication within a computer system

Though writing this out can be tedious so commonly hexadecimal format is used 

## RISC-V Fields

RISC-V fields are given names to make them easier to discuss:
![[RISC-V Fields.png]]

The naming of each field is as follows:
- *opcode*: Basic operation of the instruction
- *rd*: The register destination operand. (Gets result of the operand)
- *funct3*: an additional opcode field
- *rs1*: the first register source operand
- *rs2*: the second register source operand
- *funct7*: an additional opcode field

Though it is important to note that passing/using a constant would only allow a yield of $2^5 -1$ or 31 value since we would need to use one of the `rs` registers which is only 5 bits long

The way we get around this is by keeping our instructions the same length but having different formats for the instructions. For example the one used above is called a **R-type** (Register type) instruction and if we needed to use a constant operand then we would use the **I-type** format shown below:
![[I-type Instruction.png]]

The 12 bit *immediate* is interpreted as the 2's complement value which can be represented as the integers from $-2^{11}$ to $2^{11} -1$

If we want to load a register instruction such as 
```assembly
ld x9, 64(x22) // temp reg x9 gets A[8]
```

Then we would use the **S-type** format that is shown below:

![[S-type format.png]]

- In this case `rs2` is the source register 

Longer translation example:
```c
A[30] = h + A[30] + 1;
```
In RISC-V Assembly langauge this would look like:
```assembly
ld x9, 240(x10) //temp reg x9 gets A[30]
add x9, x21, x9 // temp reg x9 gets h+A[30]
addi x9, x9, 1 // temp reg x9 now has h + A[30] + 1
sd x9, 240(x10) // Stores h+A[30]+1 back into A[30]
```
Below are snippets of what this looks like in machine language instructions
![[Example Machine Language.png]]

# 2.6 Logical Operations

The first class of operations is called *shifts* where all they do is move bits in a doubleword to the left or the right. 

In RISC-V shift instructions for these are:
- *Shift left logical immediate*: **slli**
- *Shift right logical immediate*: **srli**

Example:
```assembly
slli x11, x19, 4 // reg x11 = reg x19 << 4 bits
```

These 2 shift instructions use the I-type format

![[ShiftMachineLanguage.png]]

Shifting to the left by `i` bits gives the identical result as multiplying by $2^i$ just as for decimal numbers shifting by i digits is equivalent to $10i$

Another type of shift is the *shift right arithmetic* **(srai)**. This one is similar to the **srli** but instead of replacing the vacant bits on the left with zeros, they are replaced with the copies of the old sign bit

RISC-V also provides variants of all three shifts that take the shift amount from a register, rather than from an immediate: **sll**, **srl**, and **sra**.

**AND**: logical bit-by-bit operation with 2 operands that calculates a 1 only if there is a 1 in both operands, sometimes referred to as a mask

**OR**: A logical bit by bit operation with two operands that calculates a 1 if there is a 1 in either operand

**NOT**: A logical bit by bit operation with one operand that inverts the bits; that is replaces each 1 with a 0 and each 0 with a 1

**XOR**: Logic bit by bit operation with 2 operands that calculates the exclusive or of the two operands. That is, calculates a 1 only if the values are different in the two operands

# 2.7 Instructions for Making Decisions

`beq`: branch if equal
```assembly
beq rs1,rs2, L1
```
This basically says go to statement `L1` if the value in register `rs1` is  equal to the value in register `rs2`

`bne`: branch not equal
```assembly
bne rs1,rs2, L1
```
This basically says go to statement `L1` if the value in register `rs1` is **not** equal to the value in register `rs2`

Example of conditional branching:
```c
if (i == j) f = g+h;
else f = g-h;
```
Commonly while it may seem intuitive to do the equal case the code is commonly more efficient if we test the opposite condition . The following RISC-V code would look like:
```assembly
bne x22, x23, Else // go to else if i \neq j
add x19, x20, x21 // f = g + h (skipped if i \neq j)
beq x0, x0, Exit // if 0 == 0 go to Exit (really just exit after add since if we hit the first condition we jump to Else:)
Else: sub x19,x20,x21 // f = g - h
Exit:
```

## Loops

**Compiling a while loop in C**
```c
while(save[i] == k)
	i+=1;
```
Here we will say that `i,k` correspond with registers `x22,x24` and the base of the array save is in `x25`. This while loop would look like this in RISC-V assembly
```assembly
Loop: slli x10, x22, 3 //temp x10 = i * 8
add x10, x10, x25 //x10 = address of save[i]
ld x9, 0(x10) // temp reg x9 = save[i]
bne x9, x24, Exit // goto exit if save[i] not = k
addi x22,x22,1 // i=i+1
beq 0x, x0, Loop // go to loop 
Exit:
```
The first step is to load `save[i]` into a temporary register. Before we can load `save[i]` into a temporary register, we need to have its address. Before we can add `i` to the base of array `save` to form the address, we must multiply the index `i `by 8 due to the byte addressing issue. Fortunately, we can use shift left, since shifting left by 3 bits multiplies by $2^3$ or 8. So we start by adding the label `Loop` so we can branch back to that instruction at the end of the loop. 

Line 2 : We get the address of `save[i]` by adding the base `x25` of the save to the temp reg `x10`

Line 3:  Now we can use the address to load `save[i]` into a temporary register

Line 4: Then we perform a loop test to see if we need to exit

Line 5: add 1 to `i`

Line 6: go back to `Loop`

**Basic Block**: A sequence of instructions without branches (except possible at the end) and without branch targets or branch levels (except possibly at the beginning)

`blt`: branch less than, which compares values of 2 registers and takes the branch if the value in the first register is smaller. 
Branch if greater than or equal (`bge`) takes the branch in the opposite case, that is, if the value in rs1 is at least the value in rs2.

Branch if less than, unsigned (`bltu`) takes the branch if the value in rs1 is smaller than the value in rs2 when the values are treated as unsigned numbers.

branch if greater than or equal, unsigned (`bgeu`) takes the branch in the opposite case.

## Bounds Check Shortcut

```assembly
bgeu x20, x11, IndexOutOfBounds // if x20>= x11 or x20 < 0, goto IndexOutOfBounds
```

## Case/Switch Statement

**Branch Table/Branch Address Table**: table of addresses of alternative instruction sequences. 
So in the case of a switch statement the program loads the appropriate entry from the branch table into a register. It then needs to branch using the address in the register.

To do this RISC-V includes an *indirect jump* instruction which performs an unconditional branch to the address specified in a register. 

# 2.8 Support Procedures in Computer Hardware

**Procedure**: just a function or a stored subroutine that performs a specific task based on the parameters with which it is provided. 

RISC-V software follows the following convention for procedure calling in allocating its 32 registers:
- `x10-x17`: eight parameter registers in which to pass parameters or return values
- `x1`: one return address register to return to the point of origin

**jump and link instruction** (`jal`): which is an instruction that branches to an address and simultaneously saves the address of the following instruction in a register. 
```assembly
jal x1, ProcedureAdress // jump to ProcedureAdress and write return address to x1
```
**return address**: a link to the calling site that allows a procedure to return to teh proper address; in RISC-V it is stored in register `x1`

To support the return from a procedure RISC-V uses a jump and link return instruction: `jalr`
```assembly
jalr x1, 0(x1)
```
The jump and link register instruction branches to the address stored in the register `x1`.
Thus the calling program or **caller** puts the parameter values in `x10-x17` and uses `jal x1, x` to branch to procedure `x` which is the **callee**. The callee then performs the calculations and places the results in the same parameter registers and returns control to the caller that is using `jalr x0, 0(x1)`

**caller**: the program which instigates a procedure and provides the necessary parameter values
**callee**: a procedure that executes a series of stored instructions based on parameters provided by the caller and then returns control to the caller. 

**Program counter (PC)**: The register containing the address of the instructions in the program being executed

## Using More Registers

Suppose we need more registers for a procedure than the eight argument registers. This means we need to spill register to memory. 
The ideal data structure for spilling registers is a **stack** (LIFO). A stack needs a pointer to the most recently allocated address in the stack to show where the next procedure should place the register to be spilled or where ol register values are found. In RISC-V the **stack pointer** is register `x2` also known as `sp`

**Stack**: A data structure for spilling registers organized as last-in first out queue
**Stack Pointer**: A value denoting the most recently allocated address in a stack that shows where registers should be spilled or where old register values can be found

**Compiling a C Procedure that doesn't call another procedure**:
```c
long long int leaf_example (long long int g, long long int h, long long int i, long long int j)
{
	long long int f;
	f = (g + h) − (i + j);
	return f;
}
```
 Here we are going to say that the variables `g,h,i,j,f` correspond to register `x10,x11,x12,x13,x20` respectively. 
We need to save three registers (2 temp) as `x5,x6,x20`. We push the old values onto the stack by creating space for three doublewords on the stack then store them
``` assembly
addi sp, sp, -24 // adjust stack to make froom for 3 items
sdx5, 16(sp) //save register x5 for use afterwards
sdx6, 8(sp) // save register x6 for use afterwards
sdx20, 0(sp) // save register x20 for use afterwards
```

These instructions correspond to teh body of the procedure:
```assembly
add x5, x10 , x11 // register x5 contains g+h
add x6, x12, x13 // register x6 contains i+j
sub x20, x5,x6 // f = x5-x6 which is (g+h) - (i+j)
```

To then retunr the value of `f` we copy it ito a parameter register:
```assembly
addi x10, x20, 0 // returns f (x10 = x20 + 0)
```
Before returning, we restore the three old values of the registers we saved by “popping” them from the stack:
```assembly
ld x20, 0(sp) // restore register x20 for caller
ld x6, 8(sp) // restore register x6 for caller
ld x5, 16(sp) // restore register x5 for caller
addi sp, sp , 24 //adjust stack to delete 3 times
```
Then the procedure will end with a branch register using the return address:
```assembly
jalr x0, 0(x1) // branch back to calling routine  
```

So really in this example we are using temp registers with the assumption that the old values must be saved and restored.
To avoid saving and restoring a register whose value is never used RISC-V software seperates 19 of the registers into 2 groupd:
1. `x5-x7` and `x28-x31`: temp registers that are not perserved by the callee on a procedure call
2. `x8 - x9` and `x18-x27`: save registers that must preserve on a procedure call 

So in the example above, since the caller does not expect registers `x5` and `x6` to be preserved across a procedure call, we can drop two stores and two loads from the code. We still must save and restore `x20`, since the callee must assume that the caller needs its value.

## Nested Procedures 

**Leaf Procedure**: a procedure that does not call other procedures

Using an example of a recursive procedure:
```c
long long int fact (long long int n)
{
	if (n < 1) return (1);
	else return (n * fact(n −1));
}
```
Here the variable `n` will correspond to the register `x10`. 
```assembly
fact:
    addi sp, sp, -16     # Adjust stack for 2 items
    sd x1, 8(sp)         # Save the return address
    sd x10, 0(sp)        # Save argument n

    addi x5, x10, -1     # x5 = n - 1
    bge x5, x0, L1       # if (n-1) >= 0, goto L1

    # Base case: return 1
    addi x10, x0, 1      # x10 = 1
    addi sp, sp, 16      # Restore stack pointer
    jalr x0, 0(x1)       # Return to caller

L1:
    addi x10, x10, -1    # n >= 1: pass (n-1) as argument
    jal fact             # Recursive call to fact(n-1)

    mv x6, x10           # Move result of fact(n-1) to x6
    ld x10, 0(sp)        # Restore original argument n
    ld x1, 8(sp)         # Restore return address
    addi sp, sp, 16      # Restore stack pointer

    mul x10, x10, x6     # Compute n * fact(n-1)
    jalr x0, 0(x1)       # Return to caller

```

## Allocating Space for New Data on The Stack
- PG227 
# Notecards
#ComputerOrganizationNotecards