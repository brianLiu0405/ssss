Lab 2 : Single Cycle CPU
========================

Architecture
------------

You can follow the architecture graph to realize a single cycle CPU.
|image1|

Operation
~~~~~~~~~

.. container:: info

   All operation are signed

.. warning::

   You must follow this ISA table to implement

Implement following instructions. RV32I ISA Layout is provided below.

-  ☒ jal
-  ☒ jalr
-  ☒ bne
-  ☒ blt
-  ☒ bge

--------------

.. warning::

   Your design must satisfy lab1 requirement

.. image:: https://hackmd.io/_uploads/HkbSaU1i3.png

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
