Lab 3 Simple Pipeline CPU
=========================

In Lab3, we will implement pipeline cpu. Don’t need to consider data
hazard and control hazard for now.

Architecture
------------

.. image:: https://hackmd.io/_uploads/S1IPbQvh2.png

Instruction
-----------

==== ==== ==
add  or   sw
addi ori  
sub  slt  
and  slti 
andi lw   
==== ==== ==

Requirement
-----------

-  implement pipeline register to store data of previous stage
-  Don’t need to consider data hazard or control hazard in this lab.
