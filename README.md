# td4.rs
4bit cpu emulator written in Rust

td4: とりあえず動作するだけの4bitCPU

# Chapter6-1
## レジスタ構成
演算とデータ移動は4bit単位で行われます。
演算用のレジスタはAとBの2つで、ほぼ同等に使用できます。
CPU外部にRAMは接続できないので、AとBレジスタはメモリ兼用。
リセット直後はA・Bレジスタ共に「0b0000」となる。

プログラムカウンタも4bitなので、プログラムは最大でも16ステップまでです。
リセット解除により「0b0000」番地の命令から順に実行されます。

フラグはC（キャリー）のみです。加算命令でキャリーが発生すると「１」になりますが、
加算命令以外のすべての命令にも影響されますので、Cフラグを参照する命令は加算命令直後に実行する必要がある。

I/Oは単純なパラレルポートで、入出力ともに4bitです。
リセット直後の出力ポートは「0b0000」です。

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

