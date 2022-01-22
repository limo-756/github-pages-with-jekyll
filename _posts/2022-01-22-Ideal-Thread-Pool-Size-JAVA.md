---
title: "Ideal Thread Pool Size In JAVA"
date: 2022-01-21
---

Factors on which ideal thread pool size depends ->
1. Type of the task - we can have following types of tasks
   a. CPU Intensive task : These task can be of numerical nature. Increasing thread pool size for these task does not lead to faster processing. multiple thread on single core will not outperform single thread on single core. Also thread in JAVA are heavy weight 1 MB in size they will incur a context-switch panelty.
   b. IO Intensive task : 
