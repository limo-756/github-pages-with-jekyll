---
title: "Kubernetes Services Types"
date: 2022-01-10
---


NodePort Service - Service listens to ports on the node and forwards that req to the pod node that is running our application (Node port service). It works for internal services only. We can specify input and target ports for the service in spec 


ClusterIP - Kubernetes creates a virtual IP to enable internal communication between services


LoadBalancer - Provision load balancer for our application in supported cloud providers. This help application to distribute load b/w pods
