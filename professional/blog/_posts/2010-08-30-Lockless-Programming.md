---
layout: blogpost
title: Lockless Programming
date: 2010-08-30
categories: [development]
music: Leona Lewis - Echo
---
There is a lot of talk and discussion about lock less programming but the reality is often lost in confusion and lack of specificity due to nomenclature. Lockless programming is a vague term that encompasses many methods and algorithmic approaches to multi threaded programming. It is most often used to imply the use of atomic operations in lieu of the standard synchronization primitives. However, it is not specific in regards to detailing if the algorithm is lock free (a thread is guaranteed to resolve in a finite number of steps) or wait free (all threads are guaranteed to resolve in a finite number of steps). In many cases, algorithms that are described as being lock less are simply re-implementing the standard synchronization primitives in atomic code. For instance, the standard critical section by Microsoft can be configured to spin on the lock check for a defined number of iterations before sleeping (context switch out). This is no different than the many spin-locks that are custom written and integrated into a "lock-less" implementation.

My expectations when using and implementing a lock less algorithm are the following:

1. The algorithm should be lock free (a thread is guaranteed to resolve in a finite number of steps)

2. In most cases, I want the implementation to guarantee order of access (it is unclear if the standard primitives do this)

3. The implementation is scalable within the expected number of concurrent executions (8-32)

4. Implementation needs to guarantee order of read-writes of the controlled data (keep in mind that the standard primitives all integrate memory fence / barriers in their execution)

5. Unnecessary data flushes are kept to a minimum (for instance, atomic operations will invalidate the entire cache line where the variable is stored)

6. Spinning should be done in such a way as to free the CPU for use by other threads / hyper threads. Yielding (context switch out) should never be done except as a fail case.
