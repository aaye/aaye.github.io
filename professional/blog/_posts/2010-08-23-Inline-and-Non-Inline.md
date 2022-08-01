---
layout: blogpost
title: Inline and Non-Inline
date: 2010-08-23
categories: [development]
music: Tim McGraw - Southern Voice
---
Performance coding is always a balance - between execution speed and resources consumed. Even achieving the desired execution speed is a balance as the increase in code complexity to achieve a certain optimization but at worse defeat the desired speed increase form the change. A general method to improve execution speed is having a function inlined - compiled directly into the calling function. Let's consider the work that is normally done when calling a function:

1. Marshall the parameters for the function onto the stack

2. Obtain the address of the function, and jump to the location.

3. Construct a stack frame for local variables

4. Perform the function execution

5. Deconstruct the stack frame

6. Marshall return values into the expected return locations (stack, or registers)

7. Return to the call function

<!--more-->

Having the code inline, compiled directly into the calling function, removes all the steps except for the actual performance of the function execution. The parameters are used directly, though it is possible copies will be made on the stack if necessary (though this will be part of the stack frame already created by the calling function). The return values are directly available to the calling function and will be used in that way. There is no jump to a new execution pointer, and no need for a jump back. In all, we have eliminated for the most part - the memory work in moving the parameters, in creating a new stack frame, and the branches caused by the instruction pointer jumps.

So what's the problem? The issue is that code is no different than data in many ways. It needs to be loaded onto the CPU for processing and execution. Inline compilation will of course cause code bloat, which will then cause more memory fetches (and cache misses) when executing the code. In performance critical code this can lead to execution slowdowns that are hard to pin down. One way of controlling this is to keep better control over what functions are inlined and which ones are not inlined. Similar to the compiler hint to inline a function, it is possible to mark functions not to be inlined.

For example, let's say you have a function that has critical performance requirements. In looking over the implementation of the function, you notice that it has two possible execution paths. However, it is noted that 95% of the time the calling functions are always in only one of the paths (possibly the second path is for initialization, over flow or other error handling). The problem is that 80% of the code is in the unused second execution path. By splitting the function into two functions - one for the primary majority case and the second containing the bulk of the code (but rarely executed), it is possible to greatly reduce the execution size of the function (increasing instruction page performance) with minimal cost.

Take Away:

1. Function inline can produce a performance increase by flattening the code compilation at the cost of code bloat.

2. There may be an advantage to extracting out large (relative) amounts of code inside of an inline function that has only a rare execution probability and placing it into a non-inline tagged secondary function to reduce the code bloat.
