---
title: "How Spring setup DB"
date: 2022-01-01
---

How Spring detect and setup DB connections?
Based on classpath dependency spring automatically detect which Database bean to configure if there is only 1 DB in the path.
Additionally you can provide url, username, password in Spring configuration to setup DB.
For H2 DB, you just neeed to provide classpath dependency as Spring automatically configure in-memory DB for you.
To start using DB, you need to create JDBCTemplate from dataSource bean.
