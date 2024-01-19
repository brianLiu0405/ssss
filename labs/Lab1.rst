Lab 1 : Single Cycle CPU
========================

Architecture
------------

You can follow the architecture graph to realize a single cycle CPU.
|image1|

Instruction
~~~~~~~~~~~

.. container:: info

   All operation are signed

Implement following instructions. RV32I ISA Layout is provided below. -
[x] add - [x] addi - [x] sub - [x] and - [x] andi - [x] or - [x] ori -
[x] slt - [x] slti - [x] lw - [x] sw - [x] beq

--------------

.. warning::

   You must follow this ISA table to implement

.. image:: https://hackmd.io/_uploads/HkbSaU1i3.png

.. raw:: html

   <!-- ## Example machine code
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
   Download this machine code =====>[TEST_INSTRUCTION.txt](https://drive.google.com/file/d/1ZjEUtUoNKgfei29mwk4N1DpltN3ITinD/view?usp=sharing)<=====
   ::: -->

Hint
----

-  Read textbook first, understand each submodule’s functionality.
-  Debugging with waveform makes your life easier.
-  Try to generate your own risc-v machine code with Ripe, you can write
   simple assembly to verify if your code runs as expect.

Reference
---------

Computer Organization and Design RISC-V Edition, CH4
`Ripes <https://github.com/mortbopet/Ripes>`__ `RISC-V
Reader <http://riscvbook.com/>`__

.. |image1| image:: https://hackmd.io/_uploads/Sy8dbBCsn.png
