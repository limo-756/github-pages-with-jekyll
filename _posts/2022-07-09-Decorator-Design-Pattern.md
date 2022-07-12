---
title: "Decorator Design Pattern"
date: 2022-07-09
---

## Intent of Decorator Pattern
When we want to extend the functionality at runtime using object composition, and we don't want to statically bind the classes.

## Motivation
1. Sometimes we want to add responsibilities to objects and not classes. Class inheritance enforce every object of that class to have inherited properties. This is inflexible because the choice is made at compile time. <br>
   Eg: GUI lets us add border to any component. If we make div class to inherit Border class then every div element will be forced to have a border. 
2. Decorator wraps the component it decorates.
3. Decorator conforms to the interface of component, so that it is transparent to the client. 
4. Decorator can perform its action before or after it delegates the control to underlying component.
5. An unlimited number of Decorator can be applied to a component.

### Decorator Pattern Structure
![Decorator Pattern Structure](../../../assets/posts/DecoratorPatternDesign.jpeg "Decorator Pattern Structure Image")

##### References :  
1. Design Patterns Elements of Reusable Object-Oriented Software
2. Head First Design Patterns
3. [Wikipedia: Decorator Pattern](https://en.wikipedia.org/wiki/Decorator_pattern)
4. [Wikipedia: Design Pattern List](https://en.wikipedia.org/wiki/Software_design_pattern)
5. [Refactoring Guru](https://refactoring.guru/design-patterns/decorator)
6. [Baeldung: The Decorator Pattern in Java](https://www.baeldung.com/java-decorator-pattern)
7. [Stackoverflow: Design Patterns with database usage](https://stackoverflow.com/questions/21541201/design-patterns-with-database-usage)
8. [Stackoverflow: Reflecting a decorator pattern in mysql database table](https://stackoverflow.com/questions/18278465/reflecting-a-decorator-pattern-in-mysql-database-table)
9. [Decorator pattern and repositories](https://blog.antoine-augusti.fr/2015/02/decorator-pattern-repositories/)
10. [Relational Database Design Patterns?](https://stackoverflow.com/questions/145689/relational-database-design-patterns)
11. [Java Magazine: The Decorator Pattern in Depth](https://blogs.oracle.com/javamagazine/post/the-decorator-pattern-in-depth)
