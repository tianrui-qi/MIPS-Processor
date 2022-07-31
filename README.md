# MIPS Processor in C

## Overview

We will implement a full gate-level circuit representing the datapath for a reduced, but still Turing complete, MIPS instruction set architecture (ISA). We first implement logic gates like and, or, not, xor, and nand and then use them to build essential componnets, including memory, control, ALU, decoder, adder, multiplexor, etc. At length, we connect them by implementing a datapath. 

## Supported Insturctions

Our ISA will include the following instructions:

| Instruction | Type   | Description         | Input format            | Operation                      | op [31-26] | func [5-0] |
|-------------|--------|---------------------|-------------------------|--------------------------------|------------|------------|
| add         | R-type | Integer addition    | add reg1 reg2 reg3      | reg1 = reg2 + reg3             | 000000     | 100000     |
| sub         | R-type | Integer subtraction | sub reg1 reg2 reg3      | reg1 = reg2 - reg3             | 000000     | 100010     |
| and         | R-type | Logical AND         | and reg1 reg2 reg3      | reg1 = reg2 & reg3             | 000000     | 100100     |
| or          | R-type | Logical OR          | or reg1 reg2 reg3       | reg1 = reg2 \| reg3            | 000000     | 100101     |
| slt         | R-type | Set less than       | slt reg1 reg2 reg3      | reg1 = (reg2 < reg3 ? 1: 0)    | 000000     | 101010     |
| jr          | R-type | Jump register       | jr reg1                 | PC = reg1                      | 000000     | 001000     |
| j           | J-type | Jump                | j address               | PC = address                   | 000010     |            |
| jal         | J-type | Jump and link       | jal address             | RA = PC, PC = address          | 000011     |            |
| beq         | I-type | Banch on equal      | beq reg1 reg2 offset    | if (reg1 == reg2) PC += offset | 000100     |            |
| addi        | I-type | Add immediate       | addi reg1 reg2 constant | reg1 = reg2 + constant         | 001000     |            |
| lw          | I-type | Load Word           | lw reg1 reg2 offset     | reg1 = M[reg2+offset]          | 100011     |            |
| sw          | I-type | Store Word          | sw reg1 reg2 offset     | M[reg2+offset] = reg1          | 101011     |            |

The “input format” given above refers to the format of the assembly instructions we’ll parse, convert to machine code, and then process through our circuit. We implement help functions to get the op codes (6-bit), register (5-bit, except J-type), and function codes (6-bit, only for R-type), and then integrate them to parse the input instructions into their 32-bit binary machine code representation. For this project, we only consider these 9 registers below:

| Register | Binary | Use                     |
|----------|--------|-------------------------|
| zero     | 00000  | Constant value 0        |
| v0       | 00010  | Return value register 0 |
| a0       | 00100  | Argument register 0     |
| t0       | 01000  | Temporary register 0    |
| t1       | 01001  | Temporary register 1    |
| s0       | 10000  | Saved register 0        |
| s1       | 10001  | Saved register 1        |
| sp       | 11101  | Stack pointer           |
| ra       | 11111  | Return address          |  


