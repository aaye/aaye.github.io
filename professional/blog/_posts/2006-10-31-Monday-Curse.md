---
layout: blogpost
title: Monday Curse
date: 2006-10-31
categories: [video games]
---
How are you realistically supposed to have the energy or the desire to get anything done on a Monday evening? Well that was my problem last night - I sat around trying to ""decide"" what to do next - read: procrastinated doing any work. Did a few compiles and fixes for the PPC build of the system - and then moved on to integrating in some external libraries into the solution so that I could watch Heroes on the other monitor. Had to get them in eventually anyway - I needed both a basic text as well as a platform specific binary load and save process. For the text (or generic) data file I decided to go with Collada. That way I would not have to reinvent the wheel, and more importantly I would never have to delve back into the ""pile"" that is the 3D Studio Max SDK. Honestly, a few rounds with razor blades would probably be more pleasant that having to use that thing ever again in my life. 

Got zlib in the solution and working. Next was libxml2 which is taking a little longer. Got most of the include path issues solved, but still have to either fix the configuration or get iConv in the solution and working. I have not decided - though I am leaning more toward iConv right now. I can see how it could be useful later for UI systems. I plan to support either UTF8 or UTF32 text streams for text output, so iConv may be useful outside of libxml2. Once its up and running I can move on to getting the Collada DOM and Implementation files up and running.
