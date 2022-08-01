---
layout: blogpost
title: Stick a Fork in It
date: 2006-11-29
categories: [development]
---
Whew. Finally done with LibXML2. I am 100% that I will have to revisit it in the future - but for now it compiles inside of its own namespace - correctly handles 32, 32/64, 64/64 and 64/32 native integer to address size issues. (ie. compiles on x86, x64 and PPC). I was a little worried about integrating in the Collada code after my experience with LibXML2 but it went in smooth as butter. It really highlighted the difference between the code bases - one professional and the other open source enthusiast. 

I finally was able to start working on the main physics engine. The first 50% of most of the common constraints have been implemented and about 90% of the solver mechanism. What is left is to complete the constraints and to design and implement a contact graph. Should be interesting. However, once again I was side tracked as I have been working on rewriting much of the math library. As it turns out on the PPC systems, because of the large number of registers on the chip, it tends to send function parameters by register. However, if the function is not inline, and uses references it forces the system to fetch the values from memory (ack!). So, I am rewriting all the routines to pass most parameters by value. At the same time I'm expanding the vector operation library to cover more of the PPC routines that are available that were not strictly implemented on XMM. I need them to be able to restrict the solver unit to a pure vectorized system.
