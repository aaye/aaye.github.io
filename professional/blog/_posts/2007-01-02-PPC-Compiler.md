---
layout: blogpost
title: PPC Compiler
date: 2007-01-02
categories: [development]
---
I was quite proud about the way I had designed my math and collision code base using templates so that it allowed for easy flexibility between float and double computations. With the native 64bit nature of the new PPC chips this could be a very strong asset for collisions that require extra precision (quadratic surfaces for instance). Then I find out that my good friend, Mr. Compiler, insists on doing a heap shuffle on each and every parameter for which a 1:1 mapping between variable and register type does not exist. For instance the compiler will not move a vector through on 4 float registers or a matrix through on 3/4 vector registers. It will insist on doing a heap shuffle - even when inlining the code (don't ask me - I'm just saying what I see on release-optimized asm output). This is enough for me to want to commit serious bodily harm on someone - the speed loss is ridiculous (for instance some hand tweaking of one loop in the code base changed my frame rate from 2FPS to 55FPS). There are times you just want to take the compiler out back for a few rounds, eh -) So as it stands the only way to get the needed efficiency would be to use #define network of math functions - since this would allow for the automatic transfer of matrix as vectors. What a pain in the ass, eh -( Anyways - going to play with it a bit more and see - but as far as I know this was never solved for the PS2 compiler either so I don't have high hopes.