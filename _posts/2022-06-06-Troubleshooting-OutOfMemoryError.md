---
title: "Troubleshooting OutOfMemoryError"
date: 2022-06-06
---

## Eclipse MAT Overview window

### Details section
It tells about size of the dump, number of classes loaded, number of objects alive and number of class loaders. <br>
If the size of the heap dump file and size of the dump in details sections does not match then that means,
that some objects are eligible for garbage collection and will be collected in next cycle.

### Pie Chart Section
It shows the distribution of retained heap memory by packages. By hovering over any of the slice see the details of the objects in the object inspector on the left. Click on any slice to drill down and follow for the outgoing references.

### Histogram Tool Option
This section shows the number of instances per class, shallow size and retained size.

#### Context Menu
We can list objects outgoing and incoming references <br>
Show shortest path to GC roots (meaning the path from thread to selected object) <br>
group by class loader, packages or superclass

### Dominator Tree
It lists the biggest objects in the heap dump. It helps to investigate which objects keep alive which objects. <br>
The dominator tree is created by doing the dfs of the graph, removing all the cycles <br>
An object x dominates an object y if every path in the object graph from the start (or the root) node to y must go through x. <br>
Dominator Tree has the following properties:
1. The objects in the sub-tree of X will be part of X's retained size.
2. Transitive association, if z dominates x and x dominates y then z dominates y.

![MAT Overview Window](../../../assets/posts/Mat_Overview_window.png "MAT Overview Window Image")

<details> 
  <summary> <h4> Difference between retained heap and shallow heap </h4> </summary>
  <p> <b> Shallow heap size </b> : It is the size of the object. 
    <br> <b> Retained heap size </b> : It is the size of the object plus size of all the objects it references that will be garbage collected if object is garbage collected. <br> </p>
    <details>
      <summary> What will be be the retained heap size of X and A in below diagram </summary>
      <p> X - 10B and A - 40B </p>
    </details>
</details>

<details>
  <summary> <h4> What is Xmx argument in Java? </h4> </summary>
  <p> The Maximum Java Heap Size (<b>Xmx</b>) argument limits the maxixmum heap size that a java program can use. <br> The default values for Xmx is based on the physical memory of the machine. <br> <b> For Java 11 and above </b> : The Xmx value is 25% of the available memory with a maximum of 25 GB. However, where there is 2 GB or less of physical memory, the value set is 50% of available memory with a minimum value of 16 MB and a maximum value of 512 MB.
<b>For Java 8</b> : The Xmx value is half the available memory with a minimum of 16 MB and a maximum of 512 MB. <br> <a href="https://blog.openj9.org/2020/04/30/default-java-maximum-heap-size-is-changed-for-java-8/"> Reference1 </a> <br> </p>
  <details> <summary> How to verify the heap size of running java programme </summary> <p> ./java -verbose:gc -version </p> </details>
</details>

<details> 
  <summary> <h4> Java command to capture heap dump automatically in application? </h4> </summary>
  <p> -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/opt/tmp/heapdump.bin <br> <a href="https://blog.heaphero.io/2017/10/13/how-to-capture-java-heap-dumps-7-options/"> Reference </a> </p>
</details>


##### References :  
1. [Youtube: Troubleshooting OutOfMemoryError - Heap dump, Eclipse MAT](https://www.youtube.com/watch?v=SuguH8YBl5g)
2. [Eclipse MAT official doc](https://help.eclipse.org/latest/index.jsp?topic=%2Forg.eclipse.mat.ui.help%2Fgettingstarted%2Fbasictutorial.html)
