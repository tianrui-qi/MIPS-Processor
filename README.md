# MIPS Processor in C

## Overview

We will implement a full gate-level circuit representing the datapath for a reduced, but still Turing complete, MIPS instruction set architecture (ISA). We first implement logic gates like and, or, not, xor, and nand and then use them to build essential componnets, including memory, control, ALU, decoder, adder, multiplexor, etc. At length, we connect them by implementing a datapath. 

## Supported Insturctions

Our ISA will include the following instructions:

| Instruction | Type   | Description         | Input format            | Operation                      |
|-------------|--------|---------------------|-------------------------|--------------------------------|
| lw          | I-type | Load Word           | lw reg1 reg2 offset     | reg1 = M[reg2+offset]          |
| sw          | I-type | Store Word          | sw reg1 reg2 offset     | M[reg2+offset] = reg1          |
| beq         | I-type | Banch on equal      | beq reg1 reg2 offset    | if (reg1 == reg2) PC += offset |
| addi        | I-type | Add immediate       | addi reg1 reg2 constant | reg1 = reg2 + constant         |
| and         | R-type | Logical AND         | and reg1 reg2 reg3      | reg1 = reg2 & reg3             |
| or          | R-type | Logical OR          | or reg1 reg2 reg3       | reg1 = reg2 \| reg3            |
| add         | R-type | Integer addition    | add reg1 reg2 reg3      | reg1 = reg2 + reg3             |
| sub         | R-type | Integer subtraction | sub reg1 reg2 reg3      | reg1 = reg2 - reg3             |
| slt         | R-type | Set less than       | slt reg1 reg2 reg3      | reg1=(reg2 < reg3? 1: 0)       |
| j           | J-type | Jump                | j address               | PC = address                   |
| jal         | J-type | Jump and link       | jal address             | RA = PC, PC = address          |
| jr          | R-type | Jump register       | jr reg1                 | PC = reg1                      |
