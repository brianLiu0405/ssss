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

.. figure:: https://hackmd.io/_uploads/HkuwstjKT.png
   :alt: 2024-01-22 14-29-38 的螢幕擷圖

   2024-01-22 14-29-38 的螢幕擷圖

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
|image1|

Instruction
~~~~~~~~~~~

.. container:: info

   All operation are signed

Implement following instructions. RV32I ISA Layout is provided below. -
add |image|

-  addi |image2|

-  sub |image3|

-  and |image4|

-  andi |image5|

-  or |image6|

-  ori |image7|

-  slt |image8|

-  slti |image9|

-  lw |image10|

-  sw |image11|

-  beq |image12|

--------------

.. warning::

   You must follow this ISA table to implement

|image13|

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

.. |image1| image:: https://hackmd.io/_uploads/Sy8dbBCsn.png
.. |image| image:: https://hackmd.io/_uploads/S1U6FtsYa.png%20=80%x
.. |image2| image:: https://hackmd.io/_uploads/ryiRcFitT.png%20=80%x
.. |image3| image:: https://hackmd.io/_uploads/ryHUqtjFa.png%20=80%x
.. |image4| image:: https://hackmd.io/_uploads/rJQdcYiFa.png%20=80%x
.. |image5| image:: https://hackmd.io/_uploads/SJ7eiKjYT.png%20=80%x
.. |image6| image:: https://hackmd.io/_uploads/BJZ9qYjta.png%20=80%x
.. |image7| image:: https://hackmd.io/_uploads/Hy3yiFiFa.png%20=80%x
.. |image8| image:: https://hackmd.io/_uploads/r1YSqKst6.png%20=80%x
.. |image9| image:: https://hackmd.io/_uploads/HJcbotjYT.png%20=80%x
.. |image10| image:: https://hackmd.io/_uploads/SJ0sctstT.png%20=80%x
.. |image11| image:: https://hackmd.io/_uploads/r1i25toYa.png%20=80%x
.. |image12| image:: https://hackmd.io/_uploads/BJIMoKiYp.png%20=80%x
.. |image13| image:: https://hackmd.io/_uploads/HkbSaU1i3.png
