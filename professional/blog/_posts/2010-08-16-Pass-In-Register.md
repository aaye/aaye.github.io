---
layout: blogpost
title: Pass In Register
date: 2010-08-16
categories: [development]
music: Brad Paisley - American Saturday Night
---
Well, apparently its been over three years since I last made a post. I was originally planning on trying to post something every week, but I am really bad when it comes to any type of regular correspondence. We'll see how long I manage to keep it going this time, eh :) 

So, as for the title - pass in register. This is an interesting thing that in some cases can be a very good performance gain but needs to be balanced against the number of available registers. On the PPC platforms (consoles) we have a ton of registers and so passing things by register is something that can be done regularly without too much forethought. However, on the PC the number of available registers is much more limited and care should be taken when using this execution path. Keep in mind as well that the optimizer for the PC platforms can often do a better job since most functions that use pass-in-register semantics are most likely inlined as well. Be careful trying to be smarter than the optimizer (even if you think - like me - that most optimizers are only slightly better than a five-year old when it comes to manipulating code). 

<!--more-->

If you have read this far, there is a good chance you are shaking your head - pass in register on the PC? When using vector (SIMD variables) most people believe that it is not possible to actually do this on the PC. As it turns out, it is possible - just a little annoying. Assuming you are using the Microsoft compiler - pass in register is done by using the native type. Be warned, type defs are not equivalent in this case. The common method for creating a cross-platform math library is to either use a type definition to cast the native type to a common name or, and the more common case, to use a structure to contain the native type (usually within a union for element access). As it turns out, there is way to convince the compiler (to my knowledge) to pass any of these in register (either the type definition or the container structure). As a matter of fact, the only way that I have found to work is to use the actual __m128 type as the variable type in the parameter. Documentation also warns that this will work only for the first three parameters. If you try to do any more than three parameters using this method, you will get the standard compiler error about being unable to guarantee variable-stack alignment requirements. 

Take away:

1. It is possible to pass in register on the PC platform.

2. Using this passing method can provide a performance boost by preventing a store-load on the stack.

3. Needs to be balanced against the usage case and the number of available registers.
