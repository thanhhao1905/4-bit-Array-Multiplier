
## Introduction to the 4-bit Array Multiplier

This repository presents a **4-bit Array Multiplier** design implemented in **Verilog**. 
This module is a fundamental yet efficient example of how to multiply two 4-bit binary numbers using the method of **partial products**.

This design is particularly useful for anyone studying computer architecture, digital logic design, or seeking a simple multiplier module to integrate into larger projects. 
The partial products are generated using **AND gates** and are then summed by a network of **full adders** arranged in an array structure, which allows for the multiplication to be performed in parallel.

### Key Features:

* **Simple and Intuitive Design:** The array structure is straightforward, accurately reflecting the pencil-and-paper multiplication algorithm.
* **Modular:** The design can be easily extended or modified to accommodate different bit-widths.
* **Easy Integration:** A standalone Verilog module that can be used in FPGA or ASIC projects.
