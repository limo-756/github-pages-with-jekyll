---
title: "Benefits of Orthogonality"
date: 2022-01-04
---

Credits: The Pragmatic Programmer by David Thomas and Andrew Hunt

What are the benefits of Orthogonality?
When components are isolated from one another we can change one without having to worry about the rest. As long as you don't change that component's external interfaces, you can be confident that you won't cause problems that ripple through the entire system.

1. Gain Productivity
1.1 Changes are localized, so development and time testing time are reduced. There is no need to keep changing existing code as you add new code.
1.2 If a component has specific and well-defined responsibility then it can be combined with new components in an intuitive, straightforward way without any side effects.
