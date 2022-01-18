---
title: "Kubernetes Pre Stop Hook"
date: 2022-01-11
---

Why do we need a pre-stop hook?
Kubernetes can stop a healthy pod when there is a rolling update or version upgrade of dependencies etc. Kubernetes stops sending traffic to your application 30 sec (can be configured) before termination so that the application terminates gracefully.
But if your application does a lot of cron jobs your application then data might get corrupted.

What does pre-stop hook do?
Kubernetes sends pre-hook notifications before termination so that your application can terminate gracefully.
Pre hook notification can be configured as an HTTP end-point or as a system command or as an shell script.

Eg of shell script: 
    lifecycle:
      preStop:
        exec:
          command: ["/bin/sh","-c","nginx -s quit; while killall -0 nginx; do sleep 1; done"]
          
          
Eg of HTTP Get req:
    lifecycle:
      preStop:
        httpGet:
          path: /pre-stop
          port: 9443
          httpHeaders:
            - name: Authorization
              value: Awesome


The following 5 steps occur when Kubernetes kills a pod:
1. The pod switches to the Terminating state and stops receiving any new traffic. Container is still running inside the pod.
2. preStop hook that is a special command or HTTP request is executed, and is sent to the container inside the pod.
   a. This is not configured currently as we don’t really need this.
3. A SIGTERM signal is sent to the pod and the container realizes that it will close soon.
4. Kubernetes waits for a grace period (terminationGracePeriodSeconds). This waiting is parallel to preStop hook and SIGTERM signal executions (default 30 sec). So, Kubernetes doesn’t wait for these to finish. If this period is finished, it goes directly to the next step.
5. SIGKILL signal is sent to the pod, and the pod is removed. If the container is still running after the grace period, the pod is forcibly removed by SIGKILL, and the termination is finished.

