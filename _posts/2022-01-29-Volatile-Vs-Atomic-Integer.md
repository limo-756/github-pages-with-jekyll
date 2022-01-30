---
title: "Volatile Vs Atomic Integer"
date: 2022-01-29
---

### What is a volatile variable? When to use a volatile variable? What is does?  
Volatile is a special keyword in java. Volatile solves the visibility problem, once the write operation is complete it makes the updated value visible to all the readers. Without volatile keyword readers could see some non-updated value  

For eg: Let's say we have 2 threads. First thread is doing some task in a loop, it checks flag value to decide when to come out of the loop. Second thread is responsible to make the flag false so that first thread doesn't get trapped in infinite loop. If we declare the flag as volatile then whenver the second thread makes it value false, then JVM will flush the updated value to shared cache and refresh all the cores cache so that they also have updated value of this flag.  
  

### What is Atomic Integer? When to use Atomic variable? What it does?
Atomic variables are thread safe, if we are updating same variable through multiple threads then due to race condition inconsistency can occur. AtomicInteger can be used for such cases.
  

##### Credits -  
1. https://www.youtube.com/watch?v=WH5UvQJizH0&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6
2. https://stackoverflow.com/questions/106591/what-is-the-volatile-keyword-useful-for
