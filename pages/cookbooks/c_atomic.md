
# C atomic operations

## 1. C11 stdatomic

The best thing to use is the c11 standard, you must `#include <stdatomic.h>` and use the keyworkd `_Atomic` before the type. 

reference [link](https://en.cppreference.com/w/c/atomic)

## 2. mintomic or turf

[mintomic](https://github.com/mintomic/mintomic) or [turf](https://github.com/preshing/turf/tree/master/turf/c) are little libraries for atomic operations in c89/c99 etc. The problem is they work only with gcc or msvc.

## 3. the volatile keyword

>In the general case volatile keeps the compiler from making optimizations related to a variable. That includes caching in registers, math optimizations, dead code elimination, etc.
>
>Under MSVC (and possibly other compilers with the right options), reading a volatile counts as an atomic acquire operation while writing one counts as an atomic release operation. These can guard against run-time memory reordering (ie, reading stale samples from the ringbuffer).

this is an info i got from [evan](https://merveilles.town/web/statuses/107919790519998847), more has to be researched.
