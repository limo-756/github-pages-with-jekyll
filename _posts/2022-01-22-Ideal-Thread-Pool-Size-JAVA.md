---
title: "Ideal Thread Pool Size In JAVA"
date: 2022-01-21
---

Factors on which ideal thread pool size depends ->
1. Number of CPU cores - How many CPU cores your application has access to, the more threads we can use to parallelize our tasks. 
2. Type of the task - we can have the following types of tasks
   a. CPU Intensive task: These tasks can be numerical in nature. Increasing thread pool size for these tasks does not lead to faster processing. multiple threads on a single-core will not outperform a single thread on a single core. Also, the thread in JAVA is heavyweight 1 MB in size they will incur a context-switch penalty.
   Hence, for CUP bound task. Ideal thread-pool size = Number of CPU cores
   b. IO Intensive task: Threads that execute these tasks are put in a wait queue by the CPU once they make an IO call. Hence thread also gets blocked with the task. If we increase the number of threads for the IO Intensive task, it will increase the throughput. 
   Ideal thread count = number of cores * (1 + wait_time/CPU_Time)
   wait_time/CPU_Time is called the blocking coefficient. It tells us how many threads we can keep to fully utilize the CPU time. For Eg: let's say CPU processing takes 10ms and IO call takes 1000ms for a given task. Then, by the time 1st thread completes its IO operation, we can provision 100 same task CPU processing.

Other factors ->
1. Are there other application running on the same server, as they will also share the same CPU and resources.
2. If your wait time is high lets say 4-5sec then as per above formulae thread count can go up to 1000's. But you can't create that many threads in the application as threads in JAVA are heavy-wait (1-2 MB). 
3. Are there any other executor in the application, as they will also share same resources.
4. Too many threads can lead to more context switching and flushing of L1/L2 cache.
