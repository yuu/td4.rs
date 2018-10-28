# td4.rs
4bit cpu emulator written in Rust

## register
| reg    | describe        | size |
|--------|-----------------|------|
| A      | A register      | 4    |
| B      | B register      | 4    |
| C      | carry flag      |      |
| input  | io port         | 4    |
| output | io port         | 4    |
| pc     | program counter | 4    |

## instruction set
| mnemonic | operation code |     |
| ---      | ---            | --- |
| ADD A,Im | 0000           |     |
| ADD B,Im | 0101           |     |
| MOV A,Im | 0011           |     |
| MOV B,Im | 0111           |     |
| MOV A,B  | 0001           |     |
| MOV B,A  | 0100           |     |
| JMP Im   | 1111           |     |
| JNC Im   | 1110           |     |
| IN  A    | 0010           |     |
| IN B     | 0110           |     |
| OUT B    | 1001           |     |
| OUT Im   | 1011           |     |

