# Lab 1 Single Cycle CPU w/ Simple RISC-V Instruction
 

## Introduction
In Lab1, you are asked to implement your Single Cycle CPU based on RISC-V ISA. After finished this lab, you should be more familiar with CPU architecture and RISC-V.

Don't be panic, this lab is not that hard as you think. To implement RISC-V CPU, you are encouraged to study what each component does, then how they coorperate. We also introduce an useful RISC-V simulator, Ripes, which can show the workflow of CPU step by step.


## Lab source code
TAs have prepare [template](https://github.com/nycu-caslab/CO2024_source/tree/main/lab1), you can follow the template or modify as you wish. However, the there are somethings you shouln't change.
- Register
- Instruction Memory
- Data Memory
- CPU I/O interface and register instance name

:::warning
The rst signal is **active low**, which means the module will reset if the rst signal is zero. And you should follow this design.
:::


## Ripes
[Ripes](https://github.com/mortbopet/Ripes) is a visual computer architecture simulator and assembly code editor built for the RISC-V instruction set architecture. Please read the document via hyperlink.

![2024-01-22 14-29-38 的螢幕擷圖](https://hackmd.io/_uploads/HkuwstjKT.png)


As the picture above, you can write you own assembly code then clock the processor, then check the right register values.

You can copy generated machine code to `TEST_INSTRUCTIONS.txt` in the following format to run your code on your CPU design. Each line in file has 8 bits, a 4 bytes instruction represented by 4 lines. The file should end with a new empty line.

```
00001010
00110000
00000100
00010011
11111111
11000001
00000001
00010011
00000000
10000001
00100000
00100011
00000000
00000000
00000100
00110011

```




-----

## Single Cycle CPU

### Architecture
You can follow the architecture graph to realize a single cycle CPU.
<!-- ![](https://hackmd.io/_uploads/r1ocUvCcn.png) -->
![](https://hackmd.io/_uploads/Sy8dbBCsn.png)


### Instruction
::: info
:bulb: All operation are signed
:::

Implement following instructions. RV32I ISA Layout is provided below.
- add
![image](https://hackmd.io/_uploads/S1U6FtsYa.png =80%x)

- addi
![image](https://hackmd.io/_uploads/ryiRcFitT.png =80%x)

- sub
![image](https://hackmd.io/_uploads/ryHUqtjFa.png =80%x)

- and
![image](https://hackmd.io/_uploads/rJQdcYiFa.png =80%x)

- andi
![image](https://hackmd.io/_uploads/SJ7eiKjYT.png =80%x)

- or
![image](https://hackmd.io/_uploads/BJZ9qYjta.png =80%x)

- ori
![image](https://hackmd.io/_uploads/Hy3yiFiFa.png =80%x)

- slt
![image](https://hackmd.io/_uploads/r1YSqKst6.png =80%x)

- slti
![image](https://hackmd.io/_uploads/HJcbotjYT.png =80%x)

- lw
![image](https://hackmd.io/_uploads/SJ0sctstT.png =80%x)

- sw
![image](https://hackmd.io/_uploads/r1i25toYa.png =80%x)

- beq
![image](https://hackmd.io/_uploads/BJIMoKiYp.png =80%x)


-----
:::warning
:warning: You must follow this ISA table to implement
:::
![](https://hackmd.io/_uploads/HkbSaU1i3.png)
<!-- 
## Example machine code
```ass
addi s0, zero, 163
addi sp, sp, -4
sw s0, 0(sp)
add s0, zero, zero
addi t0, zero, 0
LOOP:
   slti t1, t0, 7
   beq t1, zero, EXIT
   addi t0, t0, 1
   beq zero, zero, LOOP
EXIT:
    ori t1, t1, 10
    lw s0, 0(sp)
    addi sp, sp, 4
```
We can convert assembly through some software, this example uses Ripes
```
    0:  00001010001100000000010000010011
    4:  11111111110000010000000100010011
    8:  00000000100000010010000000100011
    c:  00000000000000000000010000110011
    10: 00000000000000000000001010010011
00000014 <LOOP>:
    14: 00000000011100101010001100010011
    18: 00000000000000110000011001100011
    1c: 00000000000100101000001010010011
    20: 11111110000000000000101011100011
00000024 <EXIT>:
    24: 00000000101000110110001100010011
    28: 00000000000000010010010000000011
    2c: 00000000010000010000000100010011
```
Convert machine code above to binary file like
```
00001010
00110000
...
...
00000001
00010011
```
Now you can load data into instruction memory with `$readmeh("TEST_INSTRUCTION.txt", inst_mem)` in verilog

Check if the value in register is correct or not after running your CPU.
:::warning
:warning: Download this machine code =====>[TEST_INSTRUCTION.txt](https://drive.google.com/file/d/1ZjEUtUoNKgfei29mwk4N1DpltN3ITinD/view?usp=sharing)<=====
::: -->

## Requirement
Implement your RISC-V single cycle CPU, your CPU should be able to support following RISC-V ISA
- add, addi, sub, and, andi, or, ori
- slt, slti
- lw, sw, beq

TAs have prepare verilator testbench and some `TEST_INSTRUCTION.txt` to grade your design. We will verify correctness by comparing register value, so
:::warning
:warning: Don't modify register, instruction memory and CPU interface, or you will get 0 points.
:::
:::warning
:warning: Reset signal `rst` should be active low. 
:::


## Hint
- Read textbook first, understand each submodule's functionality.
- Debugging with waveform makes your life easier.
- Try to generate your own risc-v machine code with Ripe, you can write simple assembly to verify if your code runs as expect.


## Reference
Computer Organization and Design RISC-V Edition, CH4
[Ripes](https://github.com/mortbopet/Ripes)
[RISC-V Reader](http://riscvbook.com/)
[riscv-isa-pages](https://msyksphinz-self.github.io/riscv-isadoc/html/rvi.html)
