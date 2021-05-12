---
title: SQL Server III Select, Join, Subquery, Delete, Aggregate Functions, Set Ops 
date: 05/05/2021
updated: 05/10/2021
tags: 
  - RESULT SET
  - SELECT
  - JOIN
  - Set Ops 
  - Subquery
  - Group
  - identity Column
  - DELETE/TRUNCATE
  - Aggregate Functions 
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

# Result Set

1. Result set is **a set of data,** could be empty or not, **returned by a select statement, or a stored procedure,** that is **saved in RAM or displayed on the screen**.
2. A result set is a set of records, including not only the data itself, **but also metadata like column names, types and sizes**.

A TSQL script can have 0 to multiple result sets. 

Use the following command can export the result set into file. 

​		`sqlcmd -i c:\sql\myquery.sql -o c:\sql\myoutput.txt`

# UNION, UNION ALL, Other SET Operator

1. Both SET operators. 

2. **Union** and **Union All** are all for **combining result set** (returned by a SELECT statement, or a stored procedure) together, **vertically**.

3. **UNION** **removes duplicate records** (where all columns in the results are the same), **UNION ALL does not**.
4. **Union** will **sort** the result **by the order of first column by default**, while Union will remain the original sequence by default. 

5. UNION ALL has better performance, since the database server must **do additional work to remove the duplicate rows**, but usually you do not want the duplicates (especially when developing reports).

​		*Note: When using Union and Union All, you need to make sure the numbers of columns and date type of each column from all result set should be the same.*

## Other Set Ops

		1. **INTERSECT**: Takes the data from both result sets which are in common only.
		2. **EXCEPT**: Takes the data from first result set, but not the second (i.e. no matching to each other)
		3. MINUS. 

​		*It both returns NULL set when there is no data meeting the condition.*

# JOIN

## Concept

1. Querying from More Than One Data Source 

2. The JOIN keyword allows you to **combine data from multiple tables and/or views into a single result set**. **It joins a column or columns from one table to another table, evaluating whether there is a match.** **Horizontally**

3. With the JOIN keyword, you join two tables based on a join condition. Most often you’ll see a join condition testing the equality of one column in one table compared to another column in the second table.

4. joined columns do not need to have the same name, only compatible data types.

5. SQL Server join types fall into three categories: ***inner*, *outer*, and *cross**. Self join is not a category. **Left, Right and Full are outer joins**.
6. Joins is preferred than subquery because perforemce is high.

## Difference between INNER JOIN and FULL JOIN?

Suppose you have two tables, with a single column each, and data as follows:

```sql
A    B
-    -
1    3
2    4
3    5
4    6
```

Note that (1,2) are unique to A, (3,4) are common, and (5,6) are unique to B.

### **Inner join**

An inner join using either of the equivalent queries gives the intersection of the two tables, i.e. the two rows they have in common.

```sql
select * from a INNER JOIN b on a.a = b.b;
select a.*, b.*  from a,b where a.a = b.b;

a | b
--+--
3 | 3
4 | 4
```

### **Left outer join**

A left outer join will give all rows in A, plus any common rows in B.

```sql
select * from a LEFT OUTER JOIN b on a.a = b.b;
select a.*, b.*  from a,b where a.a = b.b(+);

a |  b
--+-----
1 | null
2 | null
3 |    3
4 |    4
```

### **Right outer join**

A right outer join will give all rows in B, plus any common rows in A.

```sql
select * from a RIGHT OUTER JOIN b on a.a = b.b;
select a.*, b.*  from a,b where a.a(+) = b.b;

a    |  b
-----+----
3    |  3
4    |  4
null |  5
null |  6
```

### **Full outer join**

A full outer join will give you the union of A and B, i.e. all the rows in A and all the rows in B. If something in A doesn't have a corresponding datum in B, then the B portion is null, and vice versa.

```sql
select * from a FULL OUTER JOIN b on a.a = b.b;

 a   |  b
-----+-----
   1 | null
   2 | null
   3 |    3
   4 |    4
null |    6
null |    5
```

###  Cross join

A CROSS join produces a cartesian product, by matching up every row from the first set with every row from the second set:

```
SELECT * FROM a CROSS JOIN b 

 a   |  b
-----+-----
   1 | 		3
   1 | 		4
   1 |    5
   1 |    6
	 2 |    3
   2 |    4
  
				... and so on


```

### Self Join

Self Join is used to join a table to itself after temporally renaming. There’s not key word like “SELF JOIN”, self join is achieved by key word like “WHERE”.

​		

## Difference between Union and Join

**Union** is used to combine multiple queries into **a single query** with **all the records of queries and the same column forms**. (**Vertically**)

**Join** is used to combine data from multiple queries with the column names of all queries. The number of rows depends on the kinds of joins and the queries. (**Horizontally**)

a. **from diff tables or result set**

​		JOIN combines data from many tables based on a matched condition between them.	

​		UNION combines the result-set of two or more SELECT statements, or procedures.

b. columns or rows

​		JOIN combines data into **new columns**.	

​		UNION combines data into **new rows**

c. Number of columns

​		JOIN: Number of columns selected from each table **may not be same.**

​		UNION: Number of columns selected from each table **should be same.**

*d. 

​		Datatypes of corresponding columns selected from each table can be different.

​		Datatypes of corresponding columns selected from each table should be same.

*e.

​		It may not return distinct columns.	

​		It returns distinct rows.

# WHERE Clause, Having Clause



A WHERE clause in SQL specifies that a SQL DML statement **should only affect rows that meet specified criteria**. The criteria are expressed in the form of predicates. WHERE clauses are not mandatory clauses of SQL DML statements, but can be used to limit the number of rows affected by a SQL DML statement or returned by a query. In brief SQL **WHERE clause is used to extract only those results from a SQL statement,** such as: SELECT, INSERT, UPDATE, or DELETE statement.

A HAVING clause in SQL specifies that an SQL SELECT statement must only return rows **where aggregate values meet the specified conditions**.

WHERE is taken into account **at an earlier stage of a query execution**, **filtering the rows read from the tables**. If a query contains GROUP BY, data from the tables are grouped and aggregated. After the aggregating operation, HAVING is applied, f**iltering out the rows that don't match the specified conditions.** 

Therefore, **WHERE applies to data read from tables**, and **HAVING should only apply to aggregated data, which are not known in the initial stage of a query**.

To view the present condition formed by the GROUP BY clause, the HAVING clause is used.

WHERE could **only work on columns that already exist in original queries**, after FROM and before key words like “GROUP BY”. Having could be used on columns t**hat don’t exist in original queries, but created during the former processes**. **Having shall be written after GROUP BY** (all in specific sequence).

# SELECT Advanced

## *SELECT-OVER

Determines the **partitioning and ordering** of a **rowset** before the associated window function is applied. That is, the OVER clause defines a window or user-specified set of rows within a query result set. A window function then computes a value for each row in the window. You can use the OVER clause with functions to compute aggregated values such as moving averages, cumulative aggregates, running totals, or a top N per group results.

## SELECT-GROUP BY

A SELECT statement clause that **divides the query result into groups of rows**, usually for the purpose of performing one or more aggregations on each group. The **SELECT statement returns one row per group.**

## * **Multiple group by columns**

Yes, there could be. If there **are multiple columns following GROUP BY**, S**QL will put the rows with the same values in all those columns in the same group**.

A GROUP BY statement in SQL specifies that a SQL SELECT statement partitions result rows into groups, based on their values in one or several columns. 

Typically, grouping is used to apply some sort of aggregate function for each group.

- Group By Col_A means put all those with the same value for Col_A the one group.

- Group By Col_A, Col_B means put all those with the same values for both Col_A and Col_B in the one group.

```
		Table: Subject_Selection

		+---------+----------+----------+
		| Subject | Semester | Attendee |
		+---------+----------+----------+
		| ITB001  |        1 | John     |
		| ITB001  |        1 | Bob      |
		| ITB001  |        1 | Mickey   |
		| ITB001  |        2 | Jenny    |
		| ITB001  |        2 | James    |
		| MKB114  |        1 | John     |
		| MKB114  |        1 | Erica    |
		+---------+----------+----------+

		group by Subject :

		+---------+-------+
		| Subject | Count |
		+---------+-------+
		| ITB001  |     5 |
		| MKB114  |     2 |
		+---------+-------+

		# of rows with subject = ITB001 is 5

		group by Subject, Semester:

		+---------+----------+-------+
		| Subject | Semester | Count |
		+---------+----------+-------+
		| ITB001  |        1 |     3 |
		| ITB001  |        2 |     2 |
		| MKB114  |        1 |     2 |
		+---------+----------+-------+

		# of rows with subject = ITB001 and Semester=1 is 3
		# of rows with subject = ITB001 and Semester=2 is 2

		Therefore, it is possible group by mutiple columns. 
		
```



# Identity Column

- Identity column is autogenerated column in a table. Identity column will will not get reset to initial value incase of delete but truncate will reset value to its initial value. 
- Identity column will will not get reset to initial value incase of delete but truncate will reset value to its initial value.

The term **seed** refers to the internal value SQL Server uses to generate the next value in the sequence. 

By default, an identity column's first value is 1 and each new value increments by one (1, 2, 3, 4, and so on).

identity column generates sequential values for new records using a seed value.

An identity column is a column in a database table that is made up of values generated by the database.

- The DELETE will not reseed the identity value, the new inserted row will start with the identity with just deleted

- The TRUNCATE will reseed the identity value, the new inserted row will start with the inital value 1. 

Example:

```sql
CREATE TABLE #Person
(
	person_id INT IDENTITY(1,1) PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    gender CHAR(1) NOT NULL

)
```



# DELETE\TRUNCATE

## DELETE

Removes one or more rows from a table or view in SQL Server.

## TRUNCATE

Removes all rows from a table or specified partitions of a table, without logging the individual row deletions. 

## Difference

- TRUNCATE TABLE is similar to the DELETE statement with no WHERE clause; however, TRUNCATE TABLE is faster and uses fewer system and transaction log resources.

- Truncate reseeds identity values, whereas delete doesn't.

- Truncate removes all records and doesn't fire triggers.

- Truncate is faster compared to delete as it makes less use of the transaction log.

- Truncate is not possible when a table is referenced by a Foreign Key or tables are used in replication or with indexed views.

TRUNCATE Table_Name would remove all rows from Table_Name, without logging the individual row deletions, 

​	reseeds identity values. It would not work if a table is referenced by a Foreign Key or tables are used 

​	in replication or with indexed views.

## Delete from table_name and truncate table table_name

DELETE FROM Table_Name removes all rows from Table_Name, would not ressed identity values, If you wish the delete to be automatic, you need to change your schema so that the foreign key constraint is ON DELETE CASCADE.

TRUNCATE Table_Name would remove all rows from Table_Name, without logging the individual row deletions, reseeds identity values. It would not work if a table is referenced by a Foreign Key or tables are used in replication or with indexed views.

The DELETE command is used to remove rows from a table. A WHERE clause can be used to only remove some rows. If no WHERE condition is specified, all rows will be removed. After performing a DELETE operation you need to COMMIT or ROLLBACK the transaction to make the change permanent or to undo it. Note that this operation will cause all DELETE triggers on the table to fire.

TRUNCATE removes all rows from a table. The operation cannot be rolled back and no triggers will be fired. As such, TRUCATE is faster and doesn't use as much undo space as a DELETE.

# Subquery

The following is an example showing both a subquery `SELECT` and a join `SELECT` that return the same result set and execution plan:

```sql
USE AdventureWorks2016;
GO

/* SELECT statement built using a subquery. */
SELECT [Name]
FROM Production.Product
WHERE ListPrice =
    (SELECT ListPrice
     FROM Production.Product
     WHERE [Name] = 'Chainring Bolts' );
GO

/* SELECT statement built using a join that returns
   the same result set. */
SELECT Prd1.[Name]
FROM Production.Product AS Prd1
     JOIN Production.Product AS Prd2
       ON (Prd1.ListPrice = Prd2.ListPrice)
WHERE Prd2.[Name] = 'Chainring Bolts';
GO
```

## Nested in the outer SELECT statement

A subquery nested in the outer SELECT statement has the following components:

- A regular `SELECT` query including the regular select list components.
- A regular `FROM` clause including one or more table or view names.
- An optional `WHERE` clause.
- An optional `GROUP BY` clause.
- An optional `HAVING` clause.

The SELECT query of a subquery **is always enclosed in parentheses**. It cannot include a `COMPUTE` or `FOR BROWSE` clause, and may only include an **`ORDER BY` clause when a TOP clause is also specified**.

## Nested inside the `WHERE` or `HAVING` clause or inside another subquery

A subquery can be nested inside the `WHERE` or `HAVING` clause of an outer `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement, or inside another subquery. A subquery can appear anywhere an expression can be used, **if it returns a single value.**

If a table appears **only in a subquery and not in the outer query**, then **columns from that table cannot be included in the output** (the select list of the outer query).

## Usual Formats

- `WHERE expression \[NOT] IN (subquery)`
- `WHERE expression comparison_operator \[ANY | ALL] (subquery)`
- `WHERE \[NOT] EXISTS (subquery)`

In some Transact-SQL statements, the subquery can be evaluated as if it were an independent query. Conceptually, the subquery results are substituted into the outer query (although this is not necessarily how SQL Server actually processes Transact-SQL statements with subqueries).

There are three basic types of subqueries. Those that:

- Operate on lists introduced with `IN`, or those that a comparison operator modified by `ANY` or `ALL`.
- Are introduced with an unmodified comparison operator and must return a single value.
- Are existence tests introduced with `EXISTS`.

## Comparison operators modified by `ANY`, `SOME`, or `ALL`

Comparison operators that introduce a subquery can be modified by the keywords `ALL` or `ANY`. `SOME` is an ISO standard equivalent for `ANY`.

Subqueries introduced with a modified comparison operator return a list of zero or more values and can include a `GROUP BY` or `HAVING` clause. These subqueries can be restated with `EXISTS`.

- `>ALL` means greater than every value.
- `>ANY` means greater than at least one value, that is, greater than the minimum. So `>ANY (1, 2, 3)` means greater than 1. 

The following query provides an example of a subquery introduced with a comparison operator modified by `ANY`. It finds the products whose list prices are greater than or equal to the maximum list price of any product subcategory.

```sql
USE AdventureWorks2016;
GO
SELECT [Name]
FROM Production.Product
WHERE ListPrice >= ANY
    (SELECT MAX (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID);
GO
```

- `<>ANY` means not = a, or not = b, or not = c
- `NOT IN` means not = a, and not = b, and not = c
- `<>ALL` means the same as `NOT IN`

## EXISTS 

The NOT EXISTS in SQL Server will check the Subquery for rows existence, and if there are no rows then it will return TRUE, otherwise FALSE. Or we can simply say, SQL Server Not Exists operator will return the results exactly opposite to the result returned by the Subquery.

# Grouping and Summarizing Data

Listing the TOP n Values

Using Aggregate Functions

GROUP BY Fundamentals

Having Clause

Recommended Practices



