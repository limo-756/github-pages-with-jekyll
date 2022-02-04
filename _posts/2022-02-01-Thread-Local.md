---
title: "Thread Local"
date: 2022-02-01
---

### What is ThreadLocal? When to use it? What does it do?  
ThreadLocal in java gives us a way to thread confinement of objects for optimal use of storage and removes the need to add synchronization to global or shared objects.
ThreadLocal stores data inside of a map with the thread as the key. Hence, only 1 object per thread to optimize storage.  


Eg:  

    class ThreadSafeFormatter {
      public static ThreadLocal<SimpleDateFormat> dateFormatter = new ThreadLocal<SimpleDateFormat>() {
        @Override
        protected SimpleDateFormat initialValue() {
          return new SimpleDateFormat("yyyy-MM-dd");
        }
    
        @Ovrride
        public SimpleDateFormat get() {
          return super.get();
        }
      }
    }

  
ThreadLocal has the following userful functions:  
- Initialization of ThreadLocal : ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 1);
- To remove the value from the ThreadLocal : threadLocal.remove();
-     

### What are the drawbacks of ThreadLocal?
Manual cleaning of data is required once the thread has finished the task. As the application can use old request data for new requests. Manual cleaning of thread could be error-prone and require strict review.  
One way to over-come this limitation is to use ThreadPoolExecutor class custom hooks beforeExecute() and afterExecute() methods. Eg:

    public class ThreadLocalAwareThreadPool extends ThreadPoolExecutor {

        @Override
        protected void afterExecute(Runnable r, Throwable t) {
            // Call remove on each ThreadLocal
        }
    } 
    

##### Credits :  

1. [Defog Tech : ThreadLocal in Java](https://www.youtube.com/watch?v=sjMe9aecW_A&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6&index=2)
2. [Baeldung : An Introduction to ThreadLocal in Java](https://www.baeldung.com/java-threadlocal)
