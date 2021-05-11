---
title: SQL Server V: Index, Constraint, Normallization
date: 05/10/2021
updated: 05/11/2021
tags: 
  - SQL Server
  - Index
  - Normalization
  - Constraint
categories: SQL Server
keywords: 
description: 
top_img: 
comments: 
cover: 
toc: 
toc_number: 
copyright:
copyright_author: Shiqi Zhang
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:

---

# Subqueries

 Introduction to Subqueries
 Using a Subquery as a Derived Table
 Using a Subquery as an Expression
 Using a Subquery to Correlate Data
 Using EXISTS and NOT EXISTS

# Working with Objects 

 Creating Objects
 Altering Objects
 Renaming Objects
 Dropping Objects

# Data Integrity 

 Entity Integrity
 Referential integrity
 Different Constraints
 SQL Server Day 3 Assignment

# Trigger

## What is Trigger? What types of Triggers are there?

A trigger is a special type of stored procedure that automatically runs when an event occurs in the database server. 

Two main types of triggers based on DDL or DML events: 

The **DML** Triggers and the **DDL** triggers. The DDL triggers will be fired in response to different Data Definition Language (DDL) events, such as executing CREATE, ALTER, DROP, GRANT, DENY, and REVOKE T-SQL statements. 

The **DDL** trigger can respond to the DDL actions by preventing these changes from affecting the database, perform another action in response to these DDL actions or recording these changes that are executed against the database.

Two main types of triggers based on timing of events: After or For trigger and Instead of trigger

If the trigger is fired, a special type of virtual tables called **Inserted** and **Deleted** tables will be used to keep the data values before and after the modification. The trigger statement will work under the scope of the same transaction that fires that trigger. This means that the transaction will not be committed completely until the trigger statement is completed successfully. On the other hand, the transaction will be rolled back if the trigger statement fails.



## What are the scenarios to use Triggers?

1. When you need to build a decent audit solution.
2. When you need to validate inserted or updated data in batches instead of row by row.
3. When you need to  use triggers to implement referential integrity across databases. 
4. When you need to be sure that certain events always happen when data is inserted, updated or deleted. 
5. When you need recursion.



## What is the difference between Trigger and Stored Procedure?



**TRIGGER:-**

- Trigger executes **implicitly**. Whenever an event INSERT, UPDATE, and DELETE occurs it executed automatically.
- We **cannot define a trigger inside another trigger**.
- **Transaction statements** are not allowed in the trigger.
- We **cannot return value** in a trigger.

**STORED PROCEDURE:-**

- A Procedure executed explicitly when the user using statements such as exec, EXECUTE, etc.
- We can define procedures inside another procedure. Also, we can use functions inside the stored procedure.
- Transaction statements such as COMMIT, ROLLBACK, and SAVEPOINT are allowed in the procedure.
- Stored procedures return a zero or N value. However, we can pass values as parameters.
- Return keyword used to exit the procedure.

