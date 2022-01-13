---
title: "Java Streams"
date: 2022-01-13
---

Why use JAVA streams?
JAVA streams makes code redable by making the steps explicit and easy to change.
Eg : List<StudentScores> studentsWhoGotAGrade = studentScores.stream()
       .filter(stu -> stu.calculatePercentage() > 90.0)
       .collect(Collectors.toList());
Same code with traditional for loop

List<StudentScores> studentsWhoGotAGrade = new ArrayList<>();
for (int stuNum = 0; stuNum < studentScores.size(); stuNum++) {
  if (studentScores.get(i).calculatePercentage() > 90.0) {
    studentsWhoGotAGrade.add(studentScores.get(i));
  }
}

As we can see code using streams is more concise and clear.
Also, streams provide many useful in-build tools to enhance the performance of streams using parallelism.
