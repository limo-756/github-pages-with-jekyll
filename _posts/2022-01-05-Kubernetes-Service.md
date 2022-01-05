---
title: "Kubernetes Service"
date: 2022-01-05
---

Credits - https://www.youtube.com/watch?v=5lzUpDtmWgM

Kubernetes Service 

NodePort Service - Service listens to ports on the node and forwards that req to the pod node that is running our application (Node port service). It works for internal services only. We can specify input and target ports for the service in spec 

ClusterIP - Kubernetes creates a virtual IP to enable internal communication between services

LoadBalancer - Provision load balancer for our application in supported cloud providers. This help application to distribute load b/w pods
