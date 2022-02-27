---
title: "Locks in JAVA"
date: 2022-02-19
---

### Monitor
Every object in java is a monitor object. Monitors have a lock and wait set. Monitors allow a single thread to execute once in the critical section. JVM ensures that monitors are acquired and released automatically and atomically so that race conditions cannot occur while acquiring and releasing monitors.

### Semaphore
Semaphores are used to limit the number of concurrent threads accessing a resource.  

Types of Semaphore  
1. Counting Semaphores: It is the most simple semaphore. It is used to limit concurrent access to shared resources.
2. Bounded Semaphores: Same as counting semaphores. The acquire() and release() methods are independent of each other and it is possible to release more permits than acquired. Bounded Semaphore is bounded and cannot go beyond the upper bound.
3. Timed Semaphores: It allows access to a shared resource only for a specified time. After the timer is reset all the permits are released allowing other threads to acquire permits.
4. Binary Semaphores: Same as counting semaphore but it is binary (i.e. 0 or 1 permits allowed).

Methods in Semaphore
1. acquire(): Acquire a permit from the semaphore if available and do the rest of the processing. If the permit is unavailable then the thread is blocked and moved to the waiting queue until some other thread releases the permit or some other thread interrupts the current thread.
2. acquireUninterruptibly(): Same as acquire() method, with 1 difference that if the thread is in the waiting queue and some other thread interrupts this thread then this thread will continue to wait for a permit. But, when this thread comes out of the wait state then its interrupt status will be set
3. release(): Releases a permit and returns it to the semaphore. 1 thread waiting on this semaphore is selected and moved to the run state.
4. tryAcquire(): If the permit is available then this method acquires the permit and returns immediately with true value. If the permit is not available then this method returns immediately with false value. This method does not honor fairness, if other threads are waiting for the permit, it will acquire and return immediately.
5. tryAcquire(timeout, unit): Same as above but with a timeout. Also, this method honors fairness. Other waiting threads will get a chance to acquire a permit first.
6. availablePrmits(): Returns the number of available permits.

Uses of Semaphore
1. It is used to limit access to shared resources. Eg: We have a slow service that can handle only 3 requests at a time, we can use a Semaphore to limit access.

##### Credits :  
1. [Defog Tech: Lock's Condition class in Java](https://www.youtube.com/watch?v=N0mMm5PF5Ow&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6&index=10)
2. [Defog Tech: Semaphore in Java Concurrency](https://www.youtube.com/watch?v=shH38znT_sQ)
3. [Java Point: Java Semaphore](https://www.javatpoint.com/java-semaphore)
4. [MIT EDU: Monitors](http://web.mit.edu/javadev/doc/tutorial/java/threads/monitors.html)
5. [How to do in JAVA: Difference between lock and monitor – Java Concurrency](https://howtodoinjava.com/java/multi-threading/multithreading-difference-between-lock-and-monitor/)
