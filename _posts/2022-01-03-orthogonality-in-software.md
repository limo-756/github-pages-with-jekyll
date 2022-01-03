---
title: "Orthogonality in Software Development"
date: 2022-01-03
---

Credits: The Pragmatic Programmer by David Thomas and Andrew Hunt

What Is Orthogonality?
Like in vectors, 2 vectors that are at 90 degrees. Does not impact each other. Similarly, your code should be written in a way that all components should be orthogonal to each other i.e change in 1 component should not affect other components. For eg: Change in DB schema should not impact the user interface, likewise change in the user interface should not affect DB schema.

Why Orthogonality is important?
It helps us to design systems that are easier to design, build, test, and extend.
