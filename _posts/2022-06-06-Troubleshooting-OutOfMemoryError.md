---
title: "Troubleshooting OutOfMemoryError"
date: 2022-06-06
---

<details> 
  <summary> <h4> Difference between retained heap and shallow heap </h4> </summary>
  <p> <b> Shallow heap size </b> : It is the size of the object. 
    <br> <b> Retained heap size </b> : It is the size of the object plus size of all the objects it references that will be garbage collected if object is garbage collected. <br>
    <details>
      <summary> What will be be the retained heap size of X and A in below diagram </summary>
      <p> X - 10B and A - 40B </p>
    </details>
  </p>
</details>

<details>
  <summary> <h4> What is Xmx argument in Java? </h4> </summary>
  <p> The Maximum Java Heap Size (<b>Xmx</b>) argument limits the maxixmum heap size that a java program can use. <br> The default values for Xmx is based on the physical memory of the machine. <br> <b> For Java 11 and above </b> : The Xmx value is 25% of the available memory with a maximum of 25 GB. However, where there is 2 GB or less of physical memory, the value set is 50% of available memory with a minimum value of 16 MB and a maximum value of 512 MB.
<b>For Java 8</b> : The Xmx value is half the available memory with a minimum of 16 MB and a maximum of 512 MB. <br> <a href="https://blog.openj9.org/2020/04/30/default-java-maximum-heap-size-is-changed-for-java-8/"> Reference1 </a> <br> 
  <details> <summary> How to verify the heap size of running java programme </summary> <p> ./java -verbose:gc -version </p> </details>
  </p>
</details>

<details> 
  <summary> <h4> Java command to capture heap dump automatically in application? </summary>
  <p> -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/opt/tmp/heapdump.bin <br> <a href="https://blog.heaphero.io/2017/10/13/how-to-capture-java-heap-dumps-7-options/"> Reference </a> </p>
</details>


##### Credits :  
1. [Youtube: Troubleshooting OutOfMemoryError - Heap dump, Eclipse MAT](https://www.youtube.com/watch?v=SuguH8YBl5g)
