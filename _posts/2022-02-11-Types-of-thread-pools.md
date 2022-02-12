---
title: "Types of thread pools"
date: 2022-02-07
---

### Types of Thread Pools
1. Fixed thread pool : It has fixed number of threads and it uses a blocking queue to maintain the list of all tasks that needs to be executed.
2. Cached thread pool : It keeps a sync queue, whenever a task is submitted to it executor searches for a vacant thread and if no vacant thread found then it create a new thread. Whenever a thread completes its job it is kept alive for 60 min (configurable), if no other task is available for processing then this thread is killed.
3. 
