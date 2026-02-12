
[ ] - https://www.youtube.com/watch?v=bhpzTWtee2A

## Race condition

Happens when two or more things (usually threads) try to modify the same data at the same time.

Diffeerent code paths can take differnt amount of time and would finish in different order than expected, which can cause bugs of unintended beahviours.

Can be hard to debug or reproduce and the end result is nondeterministic

## Locking and unlocking



### Optimisation with lock and unlock

One of the techniques you used to optimise a slow system

If it is not a highly contested resource, it is fine to use. Often works in an editor context

## Memory fences



### Atomic loads and stores

