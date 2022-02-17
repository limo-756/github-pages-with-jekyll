---
title: "Types of thread pools"
date: 2022-02-07
---

### Types of Thread Pools
1. Fixed thread pool : It has fixed number of threads and it uses a blocking queue to maintain the list of all tasks that needs to be executed.
2. Cached thread pool : It keeps a sync queue, whenever a task is submitted to it executor searches for a vacant thread and if no vacant thread found then it create a new thread. Whenever a thread completes its job it is kept alive for 60 min (configurable), if no other task is available for processing then this thread is killed.
3. ForkJoin thread pool: It is special type of thread pool for fork-join kind of tasks, where task creates its sub-tasks and join them to get result. It is commonly used in finding best move in games, matrix multiplication, sorting etc. It has some special methods
  1. fork() - to create a sub-task while executing a task
  2. join() - to wait on result of the sub-task.
  3. invoke() - to create and wait on result of the sub-task  
use fork join pool:
  1. when you have a recursion type of algorithm
  2. tasks do not share common varuables
  3. No syncronisation needed
  4. No blocking IO call
5. Scheduled thread pool: It is a single threaded thread pool. Task provided to this executor is run repeatedly.

### Ways to submit tasks
1. Runnable task: we can submit a runnable task which implements Runnable interface to executor service. This type of task do not return anything to invoker once the task is executed.
2. Callable task: we can submit a callable task which implements Callable interface to executor service. This type of task return result to the invoker once the task is completed.

### Ways to shutdown a thread pool
1. shutdown() : This methods inittiates shutdown by not accepting any new tasks. Additional invocation of this method has no side effects. This method does not wait for previously submitted tasks to complete.
2. shutdownNow() : This method terminates tasks that are actively executed and are in waiting list. it return the list of all tasks that were submitted but execution was not started. This method does not guarantees to stop tasks. it uses Thread.interrupt to notify executing task to finish immediately.
3. awaitTermination(long timeout, TimeUnit unit) : This method blocks untill all the current tasks have completed or timout expires or current thread is interrupted. Whichever happens first.


##### Credits :  
1. [Defog Tech: Understanding how ForkJoinPool works](https://www.youtube.com/watch?v=5wgZYyvIVJk)
