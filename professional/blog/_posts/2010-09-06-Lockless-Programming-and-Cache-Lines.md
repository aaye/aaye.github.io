---
layout: blogpost
title: Lockless Programming and Cache Lines
date: 2010-09-06
categories: [development]
music: Katy Perry - Teenage Dream
---
Having talked about the advantages of lock less programming, now there are some things that need to be taken into account when doing the data design for these systems. Primarily, one of the major factors to consider is that any interlocked/atomic commit to a variable by necessity must invalidate the cache line on which the variable is stored. Depending on the usage case for the lock, this may require isolating the variable in question from other data by either padding the structure or by keeping the lock independent of the data itself. For example:

<code>
struct
{
SpinLock m_Spin_Lock;
int m_iData;
}
Bad_Layout[101];
</code>

<!--more-->

When we go to use the spin lock, which would require at minimum an atomic write operation it will invalidate the entire cache line that contains the spin lock. On some platforms (consoles) a cache line is 128 bytes, which would easily encompass the entire data member. So this guarantees a cache miss if we were to attempt to access the data member immediately after using the spin lock. Alternatively, we can then use a SoA approach to the problem and isolate the two members.

SpinLock g_aSpin_Lock[101];

int g_aidData [101];

This seems to be better since using the lock will no longer cause the data to be cache flushed. However, we now have a different issue - primarily the global memory layout may still cause data (or other variables) to be on the same cache line as the terminus of the spin lock arrays. More importantly, assuming that the spin lock is a standard 64 bits (8 bytes), then we will have 16 spin locks per cache line - thus, creating a possible source of contention for multiple threads attempting to lock/free items from this pool of locks. Also, keep in mind that the standard synchronization primitives automatically execute memory barriers on most platforms. It is good policy to do something similar after modifying data elements that are access controlled through atomic operations or it might create an issue where the following thread that acquires the access-control could view stale data.

Take away:

1. There is no silver bullet into concurrent programming - knowing your usage pattern and design for it and not an unknown general case is key to having a performant system.

2. Always take care with your data design - and keep in mind how that data is marshalled between memory, cache and registers.
