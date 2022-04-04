---
title: "Isolation levels in Databases"
date: 2022-04-03
---

1. Read Uncommitted : In this isolation level the transaction can read uncommitted changes done by another transaction.
2. Read Committed : In this isolation level the transaction can only read the committed changes.
3. Repeatable Read : In this isolation level the transaction keeps read lock on all the rows it references and write lock on all the rows it insert/delete/update. So no chace of repeatable read.
