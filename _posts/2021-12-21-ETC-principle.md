---
title: "How does Design Principle follow ETC principle"
date: 2021-12-22
---

Credits: The Pragmatic Programmer by David Thomas and Andrew Hunt

Challenge from The Pragmatic Programmer - Explain how does design principle follow the ETC principle?
ETC means - Easy to change

1. Single Responsibility Principle
It states that a class should only be responsible for 1 task/responsibility. Hence there should be only 1 reason to change for a class.
This principle enforces the ETC principle since on any new requirement, change will be isolated in 1 class or 1 part of the code and It will make code easy to change and prevent un-intended side effects.

2. Open closed Principle
This principle says that code should be open for extension but closed for modification. For Eg: Observer Pattern that follows this principle makes it easy to add new observers.
We should use design patterns and techniques that allow us to easily add new behavior without modification.
This principle follows the ETC principle as it promotes techniques that make code easily extendable without the need for modification. As we all know that it's much easier to add brand new code to the code base than re-writing old stuff.
Hence it follows the ETC principle.

3. Dependency inversion Principle
This principle says that you should depend on abstractions (an interface) than concrete implementations. This principle makes code easy to change as we can replace concrete implementation with any other implementation which conforms to our abstraction.

4. Interface Segregation Principle
This principle says that we should have smaller interfaces instead of 1 bulky interface. As it makes it easier for clients to depend on methods that they use.

5. Liskov substitution principle
This principle states that concrete classes should be replaceable with the base class. This principle promotes bug-free code, Hence easier to change
