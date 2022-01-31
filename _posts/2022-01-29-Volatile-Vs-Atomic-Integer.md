---
title: "Volatile Vs Atomic Integer"
date: 2022-01-29
---

### What is a volatile variable? When to use a volatile variable? What is does?  
Volatile is a special keyword in java. Volatile solves the visibility problem, once the write operation is complete it makes the updated value visible to all the readers. Without volatile keyword, readers could see some non-updated value  

For eg: Let's say we have 2 threads. The first thread is doing some task in a loop, it checks flag value to decide when to come out of the loop. The second thread is responsible to make the flag false so that the first thread doesn't get trapped in an infinite loop. If we declare the flag as volatile whenever the second thread makes its value false, then JVM will flush the updated value to the shared cache and refresh all the cores cache so that they also have the updated value of this flag.  
  

### What is Atomic Integer? When to use the AtomicInteger? What does it do?
Atomic variables are thread-safe, if we are updating the same variable through multiple threads then due to race condition inconsistency can occur. AtomicInteger can be used for such cases. AtomicInteger instructs JVM to do read & write operations atomically. Profiling shows that they Atomic variables perform better than the equivalent methods using synchronization. For example, a get() operation on an AtomicReference requires only a fetch from main memory, while an a similar operation using synchronized must first flush any values cached by threads to main memory and then perform its fetch. The AtomicXXX classes provide access to native support for compare-and-swap (CAS) operations. If the underlying system supports it, CAS will be faster than any scheme cooked up with synchronized blocks in pure Java.  

AtomicInteger has the following useful functions:
1. incrementAndGet(): This method increments the variable and gets you the updated value.  
2. decrementAndGet(): This method decrements the variable and gets you the updated value.  
3. addAndGet(int delta): This method increments the variable by delta and gets you the updated value.  
4. compareAndSet(int expected, int updated): This method checks the variable value is expected then it updates the variable to a new value else it does nothing (no error thrown).  

Use Cases of AtomicInteger :
1. AtomicInteger is used in counters to publish metrics.
2. AtomicInteger is also used in non-blocking algorithms where you don't want to use synchronization & locks, instead you want to just start the operation again from start. For eg: you are generating pseudo-random numbers and you don't want to generate the same random number twice.  

`
public class AtomicPseudoRandom extends PseudoRandom {
    private AtomicInteger seed;
    AtomicPseudoRandom(int seed) {
        this.seed = new AtomicInteger(seed);
    }

    public int nextInt(int n) {
        while (true) {
            int s = seed.get();
            int nextSeed = calculateNext(s);
            if (seed.compareAndSet(s, nextSeed)) {
                int remainder = s % n;
                return remainder > 0 ? remainder : remainder + n;
            }
        }
    }
    ...
}
`
  
  
Use cases of AtomicReference : It is used in caches, to prevent multiple threads from updating same object.


##### Credits :  

1. [Defog Tech : Using volatile vs AtomicInteger in Java concurrency](https://www.youtube.com/watch?v=WH5UvQJizH0&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6)
2. [Stackoverflow: What is the volatile keyword useful for?](https://stackoverflow.com/questions/106591/what-is-the-volatile-keyword-useful-for)
3. [Stackoverflow: Practical uses of AtomicInteger](https://stackoverflow.com/questions/4818699/practical-uses-for-atomicinteger)
4. [Pact Video](https://www.youtube.com/watch?v=-XipPj3tUu0)
5. [stackoverflow: When to use AtomicReference](https://stackoverflow.com/questions/2932505/when-to-use-atomicreference-java-is-it-really-necessary)
