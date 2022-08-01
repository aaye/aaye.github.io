---
layout: blogpost
title: LibXML2 - The Continuing Saga
date: 2006-11-06
categories: [video games,physics]
---
Information Overloading: 

Just do not do it - ever! 

I have continued to work on the LibXML2 integration. It has taken me longer than expected specifically because I keep waffling on how and if I want to integrate this particularly library. Unfortunately, it seems to be consistently updated with bug fixes so that a heavily modified integration would make re-integration of fixes a particularly annoying task. However, as it stands the code base is a slip-shod combination of implementation confusion, and a complete disregard for possible platform issues. The first time that I saw a pointer cast in this manner [(int)(long)(pointer)] I knew that people were just not quite grasping the whole issue about address casting. Simply put they were putting their faith on the fact that the ""long"" type would match the address space - or in other words - someone slammed in the long cast to avoid a compilation warning when compiling on 64bit CPUs without actually thinking about it. The subsequent int cast is just the nail in the coffin. 

<!--more-->

So let me put it out there right now - CPUs can have different address space size than their intrinsic integer size. For instances we have commodity CPUs of 32bit, 32bit with 64bit addressing, and 64 bit (ie. P4, P4 with 64EMT, and PPC64). Depending on the fact that either int or long matches your address size, is completely invalid. Just as there is a size_t standard definition, there is a intptr_t definition. intptr_t is defined as the integer value that matches the pointer (address space) size. 

After dealing with that headache, I had to deal with the fact that information overloading is used throughout much of this engine. Use of the integer type (ie. signed) value to represent data storage size so that its possible to use the single -1 value as an error flag is technically improper. From a pure implementation point of view, if your xml length exceeds 31bits, you've got issues. However, in terms of a library that is meant to be reused by others – it is better to obey the letter of the law, and not just the spirit of the law. I had the same debate when modifying the code base, and decided to obey the letter of the law and changed the size descriptors to be unsigned values - this is causing a chain of rewriting since the error flag becomes size:max. I find this a much better decision since that leaves the entire (address space - 1) as valid values - while only retaining the max value as illegal. This is reasonable since if you're trying allocate the entire address space - well, that is just bad, eh . 

So in all integrating this library has forced me to go in and re-architect many of the overall implementation decisions made through out the engine. On the up-side the internationalization tools will be useful later for localization issues. This has consumed a lot of my time and it will continue to do so for at least another week (I am guessing).
