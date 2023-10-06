---
layout: blogpost
title: Incentives, Behaviours, Culture - Post 2 - Work Hours
date: 2023-04-09
categories: [management]
---
# Sharing a Cache Line with Atomic Variables - When to be Worried?

In my Engine (see Projects), for the longest time, I have adopted a practice of being aware of sharing data in a cache line where an atomic operation is also expected to occur. A great example is the common practice of using an atomic variable as a reference count for an object. This always seemed like a bad idea, as any atomic operation will likely cause a cache flush, which would mean that any nearby data operation would cause a cache miss and stall for the time to reacquire the data from the backing store. Working on the code base today, I hit this nugget, demonstrating that my instincts held up.
Though it does cause some non-trivial amount of padding, I do encourage being mindful of how atomic variables are packed into structures (or global).

https://en.cppreference.com/w/cpp/thread/hardware_destructive_interference_size

```
__cpp_lib_hardware_interference_size = 201703
hardware_destructive_interference_size == 64
hardware_constructive_interference_size == 64
 
sizeof( OneCacheLiner ) == 64
sizeof( TwoCacheLiner ) == 128
 
oneCacheLinerThread() spent 517.83 ms
oneCacheLinerThread() spent 533.43 ms
oneCacheLinerThread() spent 527.36 ms
oneCacheLinerThread() spent 555.69 ms
oneCacheLinerThread() spent 574.74 ms
oneCacheLinerThread() spent 591.66 ms
oneCacheLinerThread() spent 555.63 ms
oneCacheLinerThread() spent 555.76 ms
Average T1 time: 550 ms
 
twoCacheLinerThread() spent 89.79 ms
twoCacheLinerThread() spent 89.94 ms
twoCacheLinerThread() spent 89.46 ms
twoCacheLinerThread() spent 90.28 ms
twoCacheLinerThread() spent 89.73 ms
twoCacheLinerThread() spent 91.11 ms
twoCacheLinerThread() spent 89.17 ms
twoCacheLinerThread() spent 90.09 ms
Average T2 time: 89 ms
 
Ratio T1/T2:~ 6.16
```
