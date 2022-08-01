---
layout: blogpost
title: x64 Registers and Calling Convention
date: 2010-09-13
categories: [development]
music: Sara Barailles - Klaidoscope Heart
---
There are two principle aspects of the x64 architecture for programmers. The obvious change is a flat 64bit memory addressing capability, but the second is a little more interesting - there are now 16 64-bit registers available on the CPU. This means that by default the MSVC compiler uses the fast call semantic for compiling 64bit programs. This convention will place the first four integer sized parameters into registers (RCX, RDX, R8, R9), floating point parameters into SIMD registers (XMM0, XMM1, XMM2, XMM3) and the remaining values on the stack. Return integer values are placed into RAX and floating point return value in XMM0. This means that 64-bit applications need potentially less stack manipulation (memory copies and marshalling into registers) than their older 32bit cousin. However, there are a few things to keep in mind - the stack pointer itself must be 16 byte aligned whenever calling a function. For example a parameter-less function needs to put the return address on the stack, but this is only an eight byte value. Thus, the stack will have to be padded by an additional eight bytes to meet the function call stack alignment requirement.
