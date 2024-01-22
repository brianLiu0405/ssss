Lab 1 Single Cycle CPU w/ Simple RISC-V Instruction
===================================================

Introduction
------------

In Lab1, you are asked to implement your Single Cycle CPU based on
RISC-V ISA. After finished this lab, you should be more familiar with
CPU architecture and RISC-V.

Don’t be panic, this lab is not that hard as you think. To implement
RISC-V CPU, you are encouraged to study what each component does, then
how they coorperate. We also introduce an useful RISC-V simulator,
Ripes, which can show the workflow of CPU step by step.

Lab source code
---------------

TAs have prepare
`template <https://github.com/nycu-caslab/CO2024_source/tree/main/lab1>`__,
you can follow the template or modify as you wish. However, the there
are somethings you shouln’t change. - Register - Instruction Memory -
Data Memory - CPU I/O interface and register instance name

.. warning::

   The rst signal is **active low**, which means the module will reset
   if the rst signal is zero. And you should follow this design.

Ripes
-----

`Ripes <https://github.com/mortbopet/Ripes>`__ is a visual computer
architecture simulator and assembly code editor built for the RISC-V
instruction set architecture. Please read the document via hyperlink.

.. figure:: images/ripes.png
   :alt: Ripes

   

As the picture above, you can write you own assembly code then clock the
processor, then check the right register values.

You can copy generated machine code to ``TEST_INSTRUCTIONS.txt`` in the
following format to run your code on your CPU design. Each line in file
has 8 bits, a 4 bytes instruction represented by 4 lines. The file
should end with a new empty line.

::

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

--------------

Single Cycle CPU
----------------

Architecture
~~~~~~~~~~~~

You can follow the architecture graph to realize a single cycle CPU.
.. image:: images/singleArch.png

Instruction
~~~~~~~~~~~

.. container:: info

   All operation are signed

Implement following instructions. RV32I ISA Layout is provided below.

- add

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |00000|00   |rs2  |rs1  |000  |rd   |01100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | add        rd,rs1,rs2

:Description:
  | Adds the registers rs1 and rs2 and stores the result in rd.
  | Arithmetic overflow is ignored and the result is simply the low XLEN bits of the result.

:Implementation:
  | x[rd] = x[rs1] + x[rs2]

- addi

add immediate

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |imm[11:0]        |rs1  |000  |rd   |00100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | addi       rd,rs1,imm

:Description:
  | Adds the sign-extended 12-bit immediate to register rs1. Arithmetic overflow is ignored and the result is simply the low XLEN bits of the result. ADDI rd, rs1, 0 is used to implement the MV rd, rs1 assembler pseudo-instruction.

:Implementation:
  | x[rd] = x[rs1] + sext(immediate)

- sub

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |01000|00   |rs2  |rs1  |000  |rd   |01100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | sub        rd,rs1,rs2

:Description:
  | Subs the register rs2 from rs1 and stores the result in rd.
  | Arithmetic overflow is ignored and the result is simply the low XLEN bits of the result.

:Implementation:
  | x[rd] = x[rs1] - x[rs2]

- and

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |00000|00   |rs2  |rs1  |111  |rd   |01100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | and        rd,rs1,rs2

:Description:
  | Performs bitwise AND on registers rs1 and rs2 and place the result in rd

:Implementation:
  | x[rd] = x[rs1] & x[rs2]

- andi

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |imm[11:0]        |rs1  |111  |rd   |00100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | andi       rd,rs1,imm

:Description:
  | Performs bitwise AND on register rs1 and the sign-extended 12-bit immediate and place the result in rd

:Implementation:
  | x[rd] = x[rs1] & sext(immediate)

- or

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |00000|00   |rs2  |rs1  |110  |rd   |01100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | or         rd,rs1,rs2

:Description:
  | Performs bitwise OR on registers rs1 and rs2 and place the result in rd

:Implementation:
  | x[rd] = x[rs1] | x[rs2]

- ori

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |imm[11:0]        |rs1  |110  |rd   |00100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | ori        rd,rs1,imm

:Description:
  | Performs bitwise OR on register rs1 and the sign-extended 12-bit immediate and place the result in rd

:Implementation:
  | x[rd] = x[rs1] | sext(immediate)

- slt

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |00000|00   |rs2  |rs1  |010  |rd   |01100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | slt        rd,rs1,rs2

:Description:
  | Place the value 1 in register rd if register rs1 is less than register rs2 when both are treated as signed numbers, else 0 is written to rd.

:Implementation:
  | x[rd] = x[rs1] <s x[rs2]

- slti

set less than immediate

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |imm[11:0]        |rs1  |010  |rd   |00100|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | slti       rd,rs1,imm

:Description:
  | Place the value 1 in register rd if register rs1 is less than the signextended immediate when both are treated as signed numbers, else 0 is written to rd.

:Implementation:
  | x[rd] = x[rs1] <s sext(immediate)

- lw

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+-----+-----+-----+-----+-----+-----+---+
  |31-27|26-25|24-20|19-15|14-12|11-7 |6-2  |1-0|
  +-----+-----+-----+-----+-----+-----+-----+---+
  |offset[11:0]     |rs1  |010  |rd   |00000|11 |
  +-----+-----+-----+-----+-----+-----+-----+---+



:Format:
  | lw         rd,offset(rs1)

:Description:
  | Loads a 32-bit value from memory and sign-extends this to XLEN bits before storing it in register rd.

:Implementation:
  | x[rd] = sext(M[x[rs1] + sext(offset)][31:0])

- sw

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+------+-----+-----+-----+-----------+-----+---+
  |31-27|26-25 |24-20|19-15|14-12|11-7       |6-2  |1-0|
  +-----+------+-----+-----+-----+-----------+-----+---+
  |offset[11:5]|rs2  |rs1  |010  |offset[4:0]|01000|11 |
  +-----+------+-----+-----+-----+-----------+-----+---+



:Format:
  | sw         rs2,offset(rs1)

:Description:
  | Store 32-bit, values from the low bits of register rs2 to memory.

:Implementation:
  | M[x[rs1] + sext(offset)] = x[rs2][31:0]

- beq

.. tabularcolumns:: |c|c|c|c|c|c|c|c|
.. table::

  +-----+---------+-----+-----+-----+--------------+-----+---+
  |31-27|26-25    |24-20|19-15|14-12|11-7          |6-2  |1-0|
  +-----+---------+-----+-----+-----+--------------+-----+---+
  |offset[12|10:5]|rs2  |rs1  |000  |offset[4:1|11]|11000|11 |
  +-----+---------+-----+-----+-----+--------------+-----+---+



:Format:
  | beq        rs1,rs2,offset

:Description:
  | Take the branch if registers rs1 and rs2 are equal.

:Implementation:
  | if (x[rs1] == x[rs2]) pc += sext(offset)


--------------

.. warning::

   You must follow this ISA table to implement

.. image:: images/ISAtable.png

Requirement
-----------

Implement your RISC-V single cycle CPU, your CPU should be able to
support following RISC-V ISA - add, addi, sub, and, andi, or, ori - slt,
slti - lw, sw, beq

TAs have prepare verilator testbench and some ``TEST_INSTRUCTION.txt``
to grade your design. We will verify correctness by comparing register
value, so 

.. warning::

   Don’t modify register, instruction memory and CPU interface, or you will get 0 points. 
   
.. warning::

   Reset signal ``rst`` should be active low. 


Hint
----

-  Read textbook first, understand each submodule’s functionality.
-  Debugging with waveform makes your life easier.
-  Try to generate your own risc-v machine code with Ripe, you can write
   simple assembly to verify if your code runs as expect.

Reference
---------

Computer Organization and Design RISC-V Edition, CH4

`Ripes <https://github.com/mortbopet/Ripes>`__

`RISC-VReader <http://riscvbook.com/>`__

`riscv-isa-pages <https://msyksphinz-self.github.io/riscv-isadoc/html/rvi.html>`__

