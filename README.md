# MIPS Processor in C

## Overview

We will implement a full gate-level circuit representing the datapath for a reduced, but still Turing complete, MIPS instruction set architecture (ISA). We first implement logic gates like and, or, not, xor, and nand and then use them to build essential componnets, including memory, control, ALU, decoder, adder, multiplexor, etc. At length, we connect them by implementing a datapath. 

## Supported Insturctions

Our ISA will include the following instructions:

| I-type      | Description         | Input format            | Operation                      |
|-------------|---------------------|-------------------------|--------------------------------|
| lw          | Load Word           | lw reg1 reg2 offset     | reg1 = M[reg2 + offset]        |
| sw          | Store Word          | sw reg1 reg2 offset     | M[reg2 + offset] = reg1        |
| beq         | Banch on equal      | beq reg1 reg2 offset    | if (reg1 == reg2) PC += offset |
| addi        | Add immediate       | addi reg1 reg2 constant | reg1 = reg2 + constant         |

| R-type      | Description         | Input format            | Operation                      |
|-------------|---------------------|-------------------------|--------------------------------|
| and         | Logical AND         | and reg1 reg2 reg3      | reg1 = reg2 & reg3             |
| or          | Logical OR          | or reg1 reg2 reg3       | reg1 = reg2 \| reg3            |
| add         | Integer addition    | add reg1 reg2 reg3      | reg1 = reg2 + reg3             |
| sub         | Integer subtraction | sub reg1 reg2 reg3      | reg1 = reg2 - reg3             |
| slt         | Set less than       | slt reg1 reg2 reg3      | reg1=(reg2 < reg3? 1: 0)       |
| jr          | Jump register       | jr reg1                 | PC = reg1                      |

| J-type      | Description         | Input format            | Operation                      |
|-------------|---------------------|-------------------------|--------------------------------|
| j           | Jump                | j address               | PC = address                   |
| jal         | Jump and link       | jal address             | RA = PC, PC = address          |

The “input format” given above refers to the format of the assembly instructions we’ll parse, convert to machine code, and then process through our circuit. We implement help functions to convert the opcode (6-bit), register (5-bit), and func (6-bit, only for R-type), and then integrate them to parse the input instructions into their 32-bit binary machine code representation. Note that for this project, we only consider these 9 registers below:
