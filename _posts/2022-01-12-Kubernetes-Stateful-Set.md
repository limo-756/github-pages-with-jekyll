---
title: "Kubernetes Stateful Set"
date: 2022-01-12
---

What applications need Kubernetes Stateful Set?
Applications like DB (MYSQL) need a sticky identity with POD. MYSQL uses master-slave architecture to synchronize data writes. All the data writes goes to the master then it is sent to slaves. Pods in a StatefulSet have a unique ordinal index and a stable network identity. The Pods' ordinals, hostnames, SRV records, and A record names remain constant, but the IP addresses associated with the Pods may change. It is important not to configure other applications to connect to Pods in a StatefulSet by IP address.

How stateful set work?
Kubernetes gives every pod a name and DNS name through which you can communicate with other pods. Also, pods are created in a sequential manner in the order of the pod name sequence. They are also deleted in sequential order.

How to connect with other active members of the statefulset?
You should query the CNAME of the headless Service (eg : nginx.default.svc.cluster.local). The SRV records associated with the CNAME will contain only the Pods in the StatefulSet that are Running and Ready.


Limitations of Statefulset
1. Scaling down of statefulset will not delete the persistence memory. This is done to ensure data safety.
2. Satefulset require a headless service for network identity and user itself have to define this headless service.
3. Satefulset are harder to roolback
