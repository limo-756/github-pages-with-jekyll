---
title: "Concurrency vs Parallelism"
date: 2022-02-05
---

### What is Parallelism?
Parallelism means literally executing tasks parallelly on different cores to speed up the execution of the program.  

### What is Concurrency?
Concurrency means executing tasks in overlapping intervals on a single or multi-core machine in no specific order. Concurrency takes the help of the time-slicing concept of OS where every thread gets a chance to execute part of its task and go to the waiting state. When the first task goes to the waiting state other threads get a chance to CPU and other computing resources like Memory based on the priority of the task. It appears to end-user tasks are getting completed in parallel

##### Credits :  

1. [Defog Tech : Concurrency vs Parallelism](https://www.youtube.com/watch?v=FChZP09Ba4E&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6&index=3)
2. [HowToDoInJava : Concurrency vs Parallelism](https://howtodoinjava.com/java/multi-threading/concurrency-vs-parallelism/)
