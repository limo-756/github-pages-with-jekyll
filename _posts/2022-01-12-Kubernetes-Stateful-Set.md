---
title: "Kubernetes Stateful Set"
date: 2022-01-12
---

What applications need Kubernetes Stateful Set?
Applications like DB (MYSQL) need a sticky identity with POD. MYSQL uses master-slave architecture to synchronize data writes. All the data writes goes to the master then it is sent to slaves.

How stateful set work?
Kubernetes gives every pod a name and DNS name through which you can communicate with other pods. Also, pods are created in a sequential manner in the order of the pod name sequence. They are also deleted in sequential order.
