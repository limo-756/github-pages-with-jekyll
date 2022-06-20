---
title: "Troubleshooting OutOfMemoryError"
date: 2022-06-06
---

### Difference between retained heap and shallow heap

### How to automate heap dump automatically on java out of memory exception

### Tips around heap size

<details>
  <summary> <h4> What is Xmx argument in Java? </h4> </summary>
  <p> The Maximum Java Heap Size (**Xmx**) argument limits the maxixmum heap size that a java program can use. <br> The default values for Xmx is based on the physical memory of the machine. <br> **For Java 11 and above** : The Xmx value is 25% of the available memory with a maximum of 25 GB. However, where there is 2 GB or less of physical memory, the value set is 50% of available memory with a minimum value of 16 MB and a maximum value of 512 MB.
**For Java 8** : The Xmx value is half the available memory with a minimum of 16 MB and a maximum of 512 MB. <br> <a href="https://blog.openj9.org/2020/04/30/default-java-maximum-heap-size-is-changed-for-java-8/"> Reference1 </a> <br> 
  <details> <summary> How to verify the heap size of running java programme </summary> <p> ./java -verbose:gc -version </p> </details>
  </p>
</details>


##### Credits :  
1. [Youtube: Troubleshooting OutOfMemoryError - Heap dump, Eclipse MAT](https://www.youtube.com/watch?v=SuguH8YBl5g)
