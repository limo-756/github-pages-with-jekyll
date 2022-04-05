---
title: "Isolation levels in Databases"
date: 2022-04-03
---

### Isolation levels in DB
1. Read Uncommitted : In this isolation level the transaction can read uncommitted changes done by another transaction.
2. Read Committed : In this isolation level the transaction can only read the committed changes.
3. Repeatable Read : In this isolation level the transaction keeps read lock on all the rows it read and write lock on all the rows it insert/delete/update. So no chace of repeatable read i.e. if the same query is executed within the transacion multiple times it will be same as it will not allow other transactions to update the rows read.
4. Serializable : The most restrictive isolation level. It takes lock on range of rows and blcoks any insert, delete and update of referenced range rows. It do not allow Phantom reads.

### What is a repeatable read?
Eg: 

### What is Phantom read? 


##### Credits :  
1. [Why do We Have Repeatable Read and Serializable Isolation Levels?](https://www.youtube.com/watch?v=xR70UlE_xbo)
2. [Wikipedia: Isolation levels in DB](https://en.wikipedia.org/wiki/Isolation_(database_systems))
