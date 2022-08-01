---
layout: blogpost
title: Xbox360 GPU functions
date: 2006-12-15
categories: [development]
---
I have been spending some time working on the Xbox360 recently working how best to use the L2 locking functionality of the hardware and the specific GPU function call in the API. Essentially they allow for greater separation between CPU and GPU execution, minimizing the number of synchronization points. This has required a rewrite of how video constants are stored and manipulated in general, keeping in mind the 64 byte alignment that is required for data transfer from the CPU to the GPU. Over all its been interesting. 

Someone emailed me recently pointing out that my html parser mangled the code drop online - dropping any code after a division symbol ( the parser was interpreting it as a failed comment ). This has been fixed and so the code base should be more reasonable now. If anyone see's any other problems, please email me! 

Implemented a basic input library through XInput. Bought myself a 360 controller for windows so that I would never have to revisit Direct Input ever again. Anyone who has ever had to create a robust and thorough solution using it will understand - its a nightmare. I understand why it was designed the way it was - a PC can have any type of input device - but from a game point of view it could drive you nuts. XInput is just a slam-bam-thank-you-ma'am in-and-out affair - its wonderful.
