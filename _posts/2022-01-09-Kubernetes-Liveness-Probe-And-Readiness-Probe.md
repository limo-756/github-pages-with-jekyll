---
title: "Kubernetes Liveness Probe and Readiness Probe"
date: 2022-01-09
---


Liveness Probe - to know when to restart a container. For example, liveness probes could catch a deadlock, where an application is running, but unable to make progress. Restarting a container in such a state can help to make the application more available despite bugs.
Liveness probes do not wait for readiness probes to succeed. If you want to wait before executing a liveness probe you should use initialDelaySeconds or a startupProbe.
Restarts the pod/container if it fails. (kills and spawning of new pod)


Readiness Probe - to know when a container is ready to start accepting traffic. A Pod is considered ready when all of its containers are ready. One use of this signal is to control which Pods are used as backends for Services. When a Pod is not ready, it is removed from Service load balancers
If you don’t specify this, k8 will start redirecting the traffic to pod as soon as the container comes in START state as. But in most cases, like in wallet-manager, the app may take some time to come up or may need to load some config before starting up etc. We therefore can use readiness probes in these cases.
Readiness probes runs on the container during its whole lifecycle. You’d think it is only needed once at the time of startup but that's not the case. Say, you lose connection to your database. You don’t want to restart the pod just yet. The readiness probe fails and the pod is temporarily removed from the load balancer. Once the  connection is established and the readiness probe succeeds, the same pod can again serve the traffic.


Credits (https://www.youtube.com/watch?v=mxEvAPQRwhw)
