---
title: "Thread Local"
date: 2022-02-01
---

### What is ThreadLocal? When to use it? What it does?  
ThreadLocal in java gives us a way to thread confinment of objects for optimal use of storage and removing the need to add syncronization to global or shared objects.
ThreadLocal creates a copy of object per thread to optimize storage. It is essential to call clear method of ThreadLocal after the request is finished.
