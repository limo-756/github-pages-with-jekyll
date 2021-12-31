---
title: "SpringBoot @SpringBootApplication annotation"
date: 2021-12-31
---

What this annotation contain?
This annotation is meta-annotaion for following spring annotation
1. @Configuration : It indicates thst file containing this annotation will be processed for bean defination generation and service req for those beans at runtime. 
3. @EnableAutoConfiguration : This annotation instructs spring to autoconfigure conditional beans depending on the classes available in the classpath.
4. @ComponentScan : It tells spring to scan our application packages starting from this package. Classes that are annotated with @Configuration, @Controller, @Service
