---
title: "Locks in JAVA"
date: 2022-02-19
---

### Monitor
Every object in java is a monitor object. On a monitor we can take locks.

### Semaphore
Semaphore are used to limit the number of concurrent threads accessing a resource.  

Methods in Semaphore
1. acquire(): Acquire a permit from the semaphore if available and do rest of the processing. If the permit is unavilable then thread is blocked and moved to waiting queue until some other thread releases the permit or some other thread interrupts the current thread.
2. release(): Releases a permit and return it to semaphore. 1 thread waiting on this semaphore is selected and awarded released semaphore.

Uses of Semnaphore
1. It is used to limit the access to shared resources. Eg: We have a slow service that can handle only 3 requests at a time, we can use a Semaphore to limit access.

##### Credits :  
1. [Defog Tech: Lock's Condition class in Java](https://www.youtube.com/watch?v=N0mMm5PF5Ow&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6&index=10)
2. [Defog Tech: Semaphore in Java Concurrency](https://www.youtube.com/watch?v=shH38znT_sQ)
