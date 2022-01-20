---
title: "Trade-offs with NoSQL"
date: 2022-01-20
---

For this blog we are taking an example of ecommerce site with tables - userCart with columns (userId, savedProducts)
eg: Partition1 - U25 : {[productId:567, productName : "N95 Mask", productImage: "/images/mkt1.jpeg"]}
Partition2 - U340 : {[productId:567, productName : "N95 Mask", productImage: "/images/mkt1.jpeg"]}
Partition3 - U562 : {[productId:521, productName : "Alto Bicycle", productImage: "/images/mkt354.jpeg"]}

Tradeoffs with NoSQL - 
1. Data Duplication: For NOSQL, as we can't do joins across different partitions, NoSQL saves all the needed data of other tables (like product in above eg) with the target table itself. Suppose, if the vendor wants to change the image URL then the application will need to make this a change for all the users that have this product in their cart.
2. Integrity checks: In NoSQL, we can't use a foreign key. We will need to take care that when a product is deleted all its associated entries in userCart are also deleted.
3. Eventual Consistency: Data between master and all slaves nodes is not copied with every write operation. NoSQL marks a write query successful even if half of the slaves write data successfully.
4. Cross partition transfers: If you want to transfer money from 1 account which is partition1 to account2 which is in partition2, you can't do these operations in a transaction across multiple partitions.
5. Data can't be partitioned on more than 1 index - In the above example, we have partitioned data based on userId. Hence, if we want to query user carts that have a balance > 500, then this query will need to run on every partition as a proxy can only partition data based on 1 index.
6. NoSQL does not support SQL features like aggregation, transaction, referential-integrity

Credits - https://www.youtube.com/watch?v=E2LIlJFEaGY

