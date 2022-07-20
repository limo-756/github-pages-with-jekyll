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

## Applicability of Decorator Pattern
1. It can be used where responsibility can be added dynamically and transparently by a caller.
2. It can be used where responsibility can be withdrawn from an object (Possibly by creating a new object from existing object without certain decorators).
3. It can be used where there are many variants possible and creating class for every variant will lead to class explosion.
4. It can be used where a class is hidden and un-available for subclassing. (In C++ 3rd party libs, we don't have access to concrete classes only to their binaries).

### Decorator Pattern Structure
![Decorator Pattern Structure](../../../assets/posts/DecoratorPatternDesign.jpeg "Decorator Pattern Structure Image")

1. Component: interface for components to which responsibility can be added dynamically.
2. Concrete Component: objects to which additional responsibilities can be added
3. Decorator: conforms to component interface and contain component object so that it can decorate the object with additional responsibilities
4. Concrete Decorator: Adds responsibilities to components

### Pros of Decorator
1. It provides more flexibility than inheritance as in inheritance we would be compelled to design class hierarchies that would encapsulate all the future extension.
   With decorator future extensions are very easy to add. Also, in some cases all lot of classes pop up in inheritance for each combination.
   In decorator only addition behaviour classes are required.
2. Inheritance is static in nature, behaviour of object cannot be changed at run time, whereas decorator can be attached/detached at run-time.

### Cons of Decorator
1. A decorator and its component aren't identical. A decorator is just a transparent enclosure. Hence, we shouldn't rely on object identity (equality, equals, getClass()) when we use decorator pattern.

### Sample Code
<pre>
   <code>
    public interface ActionComponent {
        void action();
    }

    public static class HttpCallAction implements ActionComponent {

        @Override
        public void action() {
            System.out.println("Making an http call");
        }

    }

    public interface ActionDecorator {
        void action();
    }

    public static class TimeLoggerDecorator implements ActionDecorator {
        private final ActionComponent actionComponent;

        public TimeLoggerDecorator(ActionComponent actionComponent) {this.actionComponent = actionComponent;}

        @Override
        public void action() {
            System.out.printf("Starting action at %s\n", System.currentTimeMillis());
            actionComponent.action();
            System.out.printf("Action completed at %s\n", System.currentTimeMillis());

        }
    }

    public static void main(String[] args) {
        new TimeLoggerDecorator(new HttpCallAction()).action();
    }
   </code>
</pre>

### Known uses
1. Spring and various other libs uses this pattern to add authorization to methods.
2. String @Transactional annotation is a decorator.
3. Lombok also is a type of decorator.
4. Spring Aspect Oriented Programing also uses decorator.


#### Questions
1. How can we detach Decorator from a component at run-time? <br>
   Either by creating a new object from scratch.
   Otherwise, we can implement removeDecoration() method. <br>
   [Reference](https://stackoverflow.com/questions/12239784/how-to-remove-decorated-object-from-decorator-pattern-in-java)
2. How can we restrict only 1 decorator per kind? <br>
   We can implement isDecorationPresent(decoratorClass) method, that will check if the decorator or underlying decorator is of passed type.
3. How can we save the component-decorator relationship in DB? so that we can generate the same representation later. <br>
   By creating a table that will store line item (component and decorator mapping). <br> 
   [Reference](https://stackoverflow.com/questions/18278465/reflecting-a-decorator-pattern-in-mysql-database-table)
4. Can we use Decorator pattern where decorator sequence change resulting behaviour? Where decorators are not independent of each other?
5. Can we declare more than 1 base method in component/decorator interface? <br>
   Yes we can expose more than 1 method
6. What happens with the component identity? If a component has several methods. Can we still expose them even after decorating it with decorators? <br>
   Yes

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
12. [Difference between Strategy and Decorator Pattern](https://stackoverflow.com/questions/26422884/strategy-pattern-v-s-decorator-pattern)
