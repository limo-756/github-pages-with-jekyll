---
title: "Isolation levels in Databases"
date: 2022-04-03
---

### What is Isolation property?
Isolation in DB means how and when updates made by a transaction are visible to other transactions.

### Isolation levels in DB
1. Read Uncommitted: In this isolation level, the transaction can read uncommitted changes done by another transaction.
2. Read Committed: In this isolation level, the transaction can only read the committed changes. The read lock is released as soon as the select operation is finished hence if within the same transaction the same read query is run then data might change.
3. Repeatable Read: In this isolation level the transaction keeps a read lock on all the rows it read and a write lock on all the rows it inserts/delete/updates until the end of the transaction. So no chance of repeatable read i.e. if the same query is executed within the transaction multiple times it will be the same as it will not allow other transactions to update the rows read. Since range locks are not acquired hence Phantom reads can happen.
4. Serializable: The most restrictive isolation level. It takes read as well as write locks on the range of rows and blocks any insert, delete and update of referenced range rows. It does not allow Phantom reads.

### What is a Non-repeatable read?
A non-repeatable read occurs when during the course of the transaction a row is fetched 2 times and row data differ between reads as some other transaction updated row in between the transaction.

Eg:
T1 : SELECT * FROM users WHERE id = 1;
T2 : UPDATE users SET age = 21 WHERE id = 1;
     COMMIT;
T3 : SELECT * FROM users WHERE id = 1;
     COMMIT;

### What is Phantom read? 
If in a transaction, a read query is performed 2 times then in the result of 2 queries there could be a difference of rows. As some other transactions can insert a row. This can occur when range locks are not acquired on performing a SELECT, WHERE operation.

Eg:
T1 : SELECT * FROM users WHERE age BETWEEN 10 AND 30;
T2 : INSERT INTO users(id, name, age) VALUES (3, 'Bob', 27);
     COMMIT;
T3: SELECT * FROM users WHERE age BETWEEN 10 AND 30;
     COMMIT;

##### Credits :  
1. [Why do We Have Repeatable Read and Serializable Isolation Levels?](https://www.youtube.com/watch?v=xR70UlE_xbo)
2. [Wikipedia: Isolation levels in DB](https://en.wikipedia.org/wiki/Isolation_(database_systems))
