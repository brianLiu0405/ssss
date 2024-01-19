Lab 4 : Advance Pipeline CPU
============================

Architecture
------------

.. image:: https://hackmd.io/_uploads/S1na9_i23.png

Instruction
-----------

==== ==== === ====
add  or   sw  jal
addi ori  beq jalr
sub  slt  blt 
and  slti bne 
andi lw   bgt 
==== ==== === ====

Requirement
-----------

Forwarding Unit
~~~~~~~~~~~~~~~

Forwarding Unit deals with write-use data hazard, for example, your
design should handle the following case.

.. code::

   add x1, x1, x2
   add x1, x1, x3
   add x1, x1, x4

Hazard Dectection Unit
~~~~~~~~~~~~~~~~~~~~~~

Your hazard dectection unit should insert a nop when load-use data
hazard happens

.. code::

   ld x1 0(sp)
   add x1 x1 x2

Also, flush pipeline register after branch instruction once branch is
taken. - If you follow the architecture provided above - You must
determine if branch will take or not in ID stage.
