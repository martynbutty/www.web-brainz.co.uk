---
title: Computer Memory Types
description: computer memory types and considerations from a tinyML perspective
---
Here is an overview of some common types of computer memory. Although general in nature, this page is more about considerations
you may need to make when dealing with machine learning on a microcontroller running ML perspective (TinyML).

## What is it
Computers operate on bits which can take the value zero or one.

To be more useful, these bits are grouped into bytes. One byte comprises 8 bits, which can then represent things like letters 
or weights in a neural network (NN). 

Microcontrollers and CPU's read and write bytes to memory.  A memory address is a hexadecimal value that tells the 
cpu/microcontroller etc where the memory it is looking for is located.

## Types of memory
### Flash 
Flash memory is non volatile (it won't lose the stored information when powered down). It is used to store program code, 
machine learning (ML) model weights etc. 

The process of saving to flash memory is slow and also gradually degrades the memory over time, therefore flash memory 
is better suited to read only use, and only overwritten when reprogramming (a microcontroller)
### RAM
RAM is volatile (the stored information is lost when powered off). It is used for temporary storage of variables like 
input and output buffers and intermediate tensors. RAM is much faster than flash for read/write operations, so is ideal 
for use as primary memory during code execution

### Types of RAM
#### Dynamic RAM (DRAM)
DRAM uses a single transistor and capacitor to store a bit. As the capacitor quickly loses charge, it must be periodically 
refreshed to prevent the stored information being lost. This usually occurs between read and write operations. DRAM is 
most suitable for main memory in modern computers.

#### Static RAM (SRAM)
SRAM uses six transistors to store each bit. It is able to maintain the stored information without refreshing. SRAM is 
more expensive than DRAM on account of the number of transistors required, but is faster and requires less power due to 
not needing to refresh. SRAM is therefore more suitable to caches, and is commonly used as main memory on microcontrollers.

#### Registers
A third type of RAM is a register. A special purpose register is typically for low level computing functions like the program 
counter and stack pointer. General purpose registers are used to store values and memory addresses. It is unlikely you 
will need to play around with registers as a tinyML engineer unless you are working at the assembly code level.