---
title: "Kubernetes Pods"
date: 2022-01-08
---

What are Kubernetes Pods?
A pod is a single instance of an application. A pod is the smallest object that you can create in Kubernetes. 1 POD contains only 1 application instance. A POD can contain applications with helper tools. And helper tool can refer to the application using HOSTNAME as both sare the same network space, same container, same namespace. They will born and die together. Every pod has a unique IP and is rechable by all the other pods in the cluster.

Why POD exists in Kubernetes?
Pod solves the port allocation problem, to allocate ports without any conflict. Also, POD makes it feasible to change container runtime, like if you want to change from Docker to Vagrant. It's simple as all configurations are on the POD level and we do not depend on the container.
