---
title: "The DRY principle"
date: 2021-12-24
---

Credits: The Pragmatic Programmer by David Thomas and Andrew Hunt

What is the DRY Principle
We should not duplicate knowledge in more than 1 place. As it leads to changes in multiple places. We lose info about implementation with time and sometimes knowledge gets lots as developers change jobs.
So it is necessary that whatever you code should be a single, unambiguous, authoritative representation within a system. And Dry principle is not just limited to code it applies to knowledge as well.

What is not Duplication?
When two different independent entities have the same constraints, logic, etc. then some of the code/function may match.
For Eg:
def validate_age(value):
  validate_type(value, :integer)
  validate_min_integer(value, 0)
  
def validate_quantity(value):
  validate_type(value, :integer)
  validate_min_integer(value, 0)

In this case, you should always ask yourself. Is the reason to change for both the entities could be different. If yes then it is not duplication. 

Types of Duplication
1. Code duplication
How to identify code duplication?
If for a singleton change and you need to update at 2 places and in different formats? Do you need to change the code and documentation? Or a database schema and structure that holds it?

2. Duplication in Documentation
The Internal documentation should only encapsulate why the decisions were made, engineering trade-offs, etc. It should never document how it works because it is a duplication of knowledge and whenever you need to change the code you will need to update documentation.

3. Data Duplication
For Eg:

class Line {
  Point start;
  Point end;
  double length;
}
Since length can be computed using start and end point hence it is a duplication of data. But sometimes we need to make data duplication due to performance, indexing, etc. In that case, the outside world should not be made aware of the duplication.
For Eg:
public Line(Point start, Point end) {
  this.start = start;
  this.end = end;
  this.length = calculateLength();
}

4. Interdeveloper Duplication
Sometimes developers across teams, code the same logic. American Health care software had 10,000 different versions for validation of social security numbers.
Senior software developers should periodically do software audits to find and remove this type of duplication.
