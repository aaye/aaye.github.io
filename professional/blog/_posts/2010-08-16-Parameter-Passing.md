---
layout: blogpost
title: Parameter Passing
date: 2010-08-16
categories: [development]
---
Reworked the entire code base so that parameters are declared using a specific syntax so as to let me toggle whether certain types (specifically vectors and matrices) are passed by value or by reference. This is so that on the console environments I can pass things by value but keep passing them by reference on the PC platform. Fun... not! 

Tried installing Vista x64 since its got so much bling it must be a great platform to work on, right? I mean you have to use it if you want to play around with DX10. I'm sure people looking at the puss infected plague victims had the same thoughts, because really it was almost that bad. I couldn't even get the system to run the x64 version of the software. What a waste of time. Guess I'll give it the standard two year wait before even thinking of moving to the new MS OS since that is how long it seems to take them to get a decent development platform made that works on them. Bleh! 

Concentrating on the physics platform for now and continuing to write constraint software. One thing left to do before moving onto that which is finalizing a working compilation again - had to change the return values for many functions, to choose like the parameters, to pass return values by value or by constant reference. Hopefully that will not take long. My development box is back to Win XP x64 so things should go smoothly tonight.
