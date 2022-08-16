---
layout: default
include_header: true
title: Projects Managed by Andrew Aye
---

<div class="aaye-main-cv-content-title"><span class="content-title-h1"><span>GitHub Projects</span></span></div>

<div class="aaye-main-cv-content-title"><span class="content-title-h3"><span>Teikitu</span></span></div>

<a href="https://github.com/aaye/teikitu_release">GitHub Link</a>

I started this project while I was still in high school. I honestly do not think a single line of code from that original project is still in the code base. I wanted to write an engine (even then, I was more interested in writing the platform than the game itself) that mimicked the capabilities of the gold box AD&D video games. In University, after the launch of Windows 95, I then adapted the code base to be a fully COM-compliant implementation. I continued to grow the feature set of the engine in between jobs and during lulls at work. The next major update was a collision library and physics simulation. However, troubleshooting issues required an easy way to test in both 32bit and 64bit floating-point to identify numerical precision issues. Once I had completed all the math and collision routines, I found that the Microsoft compiler could not complete an optimized compilation. The problem was that I had used templates to allow for the easy shift between the different precisions. I took the opportunity to create a new implementation that was entirely ANSI C. This version is compiled in a fraction of the time (both in debug and release). Since this was a personal project, iteration time on the code base was one of my highest priorities. I made the change and continued the implementation in ANSI C. I have recently updated to C-STD 17, primarily because of the easy atomic support. ASM-level comparisons of the results from both C++ and C compilers, I find that the C optimizer has a higher chance of creating optimal code. It is not the fault of the C++ optimizers. The issue lies in the complexity of the C++ language. The compiler has to allow for a wide range of edge cases that create problems during the optimization phase. My experience has also demonstrated that when working on new embedded devices (game consoles), there is a stronger guarantee of fully functional C compilers on new embedded platforms than a C++ compiler. The issues that we had with the PS3 C++ compiler are still hallmarked anecdotes for those of us who survived that period.


<!-- CMake fork. I will occasionally rebase my changes to the main branch by Kitware. These changes are critical to my workflow for the Teikitu project. -->
