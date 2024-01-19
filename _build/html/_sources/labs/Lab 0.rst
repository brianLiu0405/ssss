Lab 0 : Environment Setup & simple verilog practice
===================================================

Verilator
---------

`Verilator <https://www.veripool.org/verilator/>`__ is an open-source
Verilog simulation tool that you will use for RTL functional simulation
to validate the RTL code you have written.

Installation
~~~~~~~~~~~~

-  How to install : https://verilator.org/guide/latest/install.html
   (Recommended to install in the Ubuntu environment.)

.. code::

   # Prerequisites:
   sudo apt-get install git perl python3 make autoconf g++ flex bison ccache
   sudo apt-get install libgoogle-perftools-dev numactl perl-doc
   sudo apt-get install libfl2  # Ubuntu only (ignore if gives error)
   sudo apt-get install libfl-dev  # Ubuntu only (ignore if gives error)
   sudo apt-get install zlibc zlib1g zlib1g-dev  # Ubuntu only (ignore if gives error)
    
   git clone https://github.com/verilator/verilator   # Only first time
    
   # Every time you need to build:
   unsetenv VERILATOR_ROOT  # For csh; ignore error if on bash
   unset VERILATOR_ROOT  # For bash
   cd verilator
   git pull         # Make sure git repository is up-to-date
   git tag          # See what versions exist
   git checkout v5.008  # Switch to specified release version
    
   autoconf         # Create ./configure script
   ./configure      # Configure and create Makefile
   make -j `nproc`  # Build Verilator itself (if error, try just 'make')
   sudo make install

-  You need to install version **5.008**. After a successful
   installation, run the following command to check if the installation
   was successful and if the version is correct.

.. code::

   verilator --version

-  The Verilator manual contains a `C++
   example <https://verilator.org/guide/latest/example_cc.html#example-c-execution>`__
   that you can locate. Follow the steps in the example to learn how to
   use it.

Full Adder & ALU
----------------

`Report <https://hackmd.io/yqWJmbX_SfOnYJNLvbjx5Q>`__ ### 1. Full Adder
Based on the circuit of the following adder, complete the circuit using
Verilog, and create a testbench using Verilator to verify the circuit.

.. image:: https://hackmd.io/_uploads/Sk7Otri9n.png

2. 4-bits ALU
~~~~~~~~~~~~~

Based on the ALU function table below, complete the full ALU circuit
using Verilog, and create a testbench using Verilator to verify the
circuit.

.. code:: verilog

   // file name : alu.v
   // You shouldn't change interface naming; otherwise, your lab0 will receive 0 points.
   module alu(input signed [3:0] a,
              input signed [3:0] b,
              input [2:0] s,
              output reg signed [3:0] y);

   // implement your module here

   endmodule

.. warning::

   The **ADD** and **SUB** operations in the ALU must use the
   completed full adder circuit.

.. warning::

   All operations are **signed** arithmetic.

.. image:: https://hackmd.io/_uploads/S1vnnvs93.png

--------------

Debug tool
----------

GTKwave
~~~~~~~

https://gtkwave.sourceforge.net/

Verilator support waveform tracing, enable waveform tracing through add
code in **testbench (cpp file)** and compile add **flag –trace**

Using GTKwave to open **.vcd** file to check the waveform

.. code:: python

   1.
   gtkWave # open UI directly

   or

   2.
   gtkwave xxx.vcd # open UI with waveform

.. image:: https://hackmd.io/_uploads/Byh7iVCih.png

Reference
---------

-  `verilator用法 <https://itsembedded.com/dhd/verilator_1/>`__
