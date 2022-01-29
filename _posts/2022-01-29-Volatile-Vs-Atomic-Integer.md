---
title: "Volatile Vs Atomic Integer"
date: 2022-01-29
---

### What is a volatile variable? When to use a volatile variable? What is does?  
Volatile is a special keyword in java. Volatile solves the visibility problem, it instructs JVM to flush down the variable value down to the shared cache so that other threads read the updated value.  
For eg: Let's say we have a producer and consumer who only operate on a single item. They share a flag variable isAvailable that is set to true by the producer once the item is ready and then the producer goes to sleep. The consumer is checking this variable in an infinite loop, as soon, as it becomes true it starts consuming.  

The problem here is that both producer and consumer are running on separate threads. Hence, the producer thread could update the local cache but the consumer cannot read the updated value.  

#### Credits - https://www.youtube.com/watch?v=WH5UvQJizH0&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6
