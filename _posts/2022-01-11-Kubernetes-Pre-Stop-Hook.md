---
title: "Kubernetes Pre Stop Hook"
date: 2022-01-11
---

Why do we need a pre-stop hook?
Kubernetes can stop a healthy pod when there is a rolling update or version upgrade of dependencies etc. Kubernetes stops sending traffic to your application 30 sec (can be configured) before termination so that the application terminates gracefully.
But if your application does a lot of cron jobs your application then data might get corrupted.

What does pre-stop hook do?
Kubernetes sends pre-hook notifications before termination so that your application can terminate gracefully.
Pre hook notification can be configured as an HTTP end-point or as a system command or as an env variable.

