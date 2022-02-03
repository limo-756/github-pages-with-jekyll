---
title: "Thread Local"
date: 2022-02-01
---

### What is ThreadLocal? When to use it? What it does?  
ThreadLocal in java gives us a way to thread confinment of objects for optimal use of storage and removing the need to add syncronization to global or shared objects.
ThreadLocal creates a copy of object per thread to optimize storage. It is essential to call clear method of ThreadLocal after the request is finished.  
ThreadLocal stores data inside of a map with the thread as the key.

Eg:  

`
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

`

What are the drawbacks of ThreadLocal?
Manual cleaning of data is required once the thread has finished the task. This could be error-prone and require strict review.  
One way to over-come this limitation is to use ThreadPoolExecutor class custom hooks beforeExecute() and afterExecute() methods. Eg:

`
    public class ThreadLocalAwareThreadPool extends ThreadPoolExecutor {

        @Override
        protected void afterExecute(Runnable r, Throwable t) {
            // Call remove on each ThreadLocal
        }
    }
`
