---

title: SEP II Transact-SQL, Querying Tools, Retrieving Data
date: 05/04/2021
updated: 
tags: 
  - notes
  - SEP
  - Full-Stack
  - Transact-SQL
categories: SEP
keywords: 
  - java
  - oop
  - leetcode
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

# General Concepts

## Database definition

Organized collection of logically related data

## Data

Known facts
Types: text, graphics, images, sound, videos

## Database management system (DBMS)

Software package for defining and managing a database. 

Examples:
Proprietary: MS Access, MS SQL Server, DB2, Oracle, Sybase

Open source: MySql, PostgreSQL

Relational database and non-relational database

## **Types Of DBMS**

- **With respect to the need and requirement of users in industry, different types of Database Management Systems were introduced to let the compatibility of user’s requirement match with the types of DBMS(Database Management Systems) available.**
- **These types of databases are generated and introduced on the basis of certain requirement parameters and technology changes. Some of them are listed below.**



![Types Of DBMS](https://minigranth.in/images/tutorials/DBMS%20IMAGES/Types%20of%20DBMS.jpeg)
**Types Of DBMS**



### **1. Types Of DBMS: File Processing System**

- **File Processing System is a traditional approach to storing and managing data. Data Storage was being done by storing the information in files present on the computer. If in case there is a need for data, the files were checked individually to retrieve desired results.**
- **For small-scaled data, the file processing system was a good option to store, manipulate, and retrieve data. But when the size of data increases, the file processing system was so slow to generate desired results and it lagged behind. It was a tough job file processing system to input such a large data in the form of files and completely impossible to retrieve data just by simply searching it in every file.**
- **Other problems of file processing system include data duplicity(redundancy), low security of data, inability to handle multiple user requests at the same time, and many more. That is why the file processing system was left out and other databases are being used now.**



### **2. Types Of DBMS: Relational Database Management System(RDBMS)**

- **In Relational Database Management Systems, unlike file processing systems the data is stored in the tables(having rows and columns) where any table can be related or linked to any other table using certain concepts. Also, data storage using tables makes it very easy to maintain, manage, and manipulate records.**
- **The data stored in tables are presented as relation and this data can be extracted and retrieved at any point in time. This can be done by using query languages such as [SQL(Structured Query Language)](https://minigranth.in/sql-tutorial/sql-introduction) which helps in data manipulation and data extraction.**



![Types Of DBMS : RDBMS](https://minigranth.in/images/tutorials/DBMS%20IMAGES/Types%20of%20DBMSRDBMS.jpeg)
**Types Of DBMS: RDBMS**



### **3. Types Of DBMS: Network Database Management System(NDBMS)**

- **Network Database Management System is another type that was very popular in the late 1970s. These databases were known to be very adaptable and flexible in terms of data storage because of their data storage architecture. But, the problem aroused at the time of data retrieval as their flexibility became the major issue.**
- **Every dataset being related to every other data set forming a network made it very complex and difficult to search and get back the required data. Hence, they were also avoided and are not being used now.**



![Types Of DBMS : NDBMS](https://minigranth.in/images/tutorials/DBMS%20IMAGES/NDBMS.jpeg)
**Types Of DBMS: NDBMS**



### **4. Types Of DBMS: Hierarchical Database Management System(HDBMS)**

- **The Hierarchical Database Management System works on the concept similar to that of “[Concept Hierarchy](https://minigranth.in/data-warehouse-tutorial/data-warehouse-architecture)”. The whole database is structured and architecture in the form similar to the structure of a tree, making it one of the simplest and fastest databases present out there.**



![Types Of DBMS : HDBMS](https://minigranth.in/images/tutorials/DBMS%20IMAGES/HDBMS.jpeg)
**Types Of DBMS: HDBMS**



### **5. Types Of DBMS: Object-Oriented Database Management System(OODBMS)**

- **They are different from other databases as Object-Oriented Database Management Systems revolves around “Object”(An object here referred to any real-world entity) and is based upon the concept of various object-oriented languages such as “C++, Java” etc.**
- OODBMS also pertains the concepts of:
  1. **Encapsulation.**
  2. **Inheritance.**
  3. **Overloading.**
  4. **Overriding.**
- **OnNotes, Poet, EyeDB are some of the examples of OODBMS**



#  SQL Server Services

The relational database server is implemented as the SQL Server service. It receives queries from users, executes them, sends responses to calling applications, and manages data in database files 

##   SQL Server Agent 

  SQL Server Agent is an automation service that manages the scheduled execution of tasks and notifies administrators of problems that occur on the server.

##   SQL Server Browser

##   SQL Server Integration Services

Integration Services provide **ETL (extract, transform, and load)** functionality that replaces Data Transformation Services (DTS) from previous versions of SQL Server. Users can create packages for extracting, transforming, and loading data from one data source to another 

##   SQL Server Analysis Services

 Analysis Services is a service that implements infrastructure for On-Line Analytical Processing (OLAP) and data mining. 

**Online analytical processing**, or **OLAP** ([/ˈoʊlæp/](https://en.wikipedia.org/wiki/Help:IPA/English)), is an approach to answer [multi-dimensional analytical](https://en.wikipedia.org/wiki/Multi-dimensional_analytical) (MDA) queries swiftly in [computing](https://en.wikipedia.org/wiki/Computing).[[1\]](https://en.wikipedia.org/wiki/Online_analytical_processing#cite_note-Codd1993-1) OLAP is part of the broader category of [business intelligence](https://en.wikipedia.org/wiki/Business_intelligence), which also encompasses [relational databases](https://en.wikipedia.org/wiki/Relational_database), report writing and [data mining](https://en.wikipedia.org/wiki/Data_mining).[[2\]](https://en.wikipedia.org/wiki/Online_analytical_processing#cite_note-2) Typical applications of OLAP include [business reporting](https://en.wikipedia.org/wiki/Business_reporting) for sales, [marketing](https://en.wikipedia.org/wiki/Marketing), management reporting, [business process management](https://en.wikipedia.org/wiki/Business_process_management) (BPM),[[3\]](https://en.wikipedia.org/wiki/Online_analytical_processing#cite_note-3) [budgeting](https://en.wikipedia.org/wiki/Budget) and [forecasting](https://en.wikipedia.org/wiki/Forecasting), [financial reporting](https://en.wikipedia.org/wiki/Financial_reporting) and similar areas, with new applications emerging, such as [agriculture](https://en.wikipedia.org/wiki/Agriculture).[[4\]](https://en.wikipedia.org/wiki/Online_analytical_processing#cite_note-ahsan-4)

## Reporting Services

Reporting Services is a system for design and delivery of relational and OLAP reports that works on top of SQL Server and IIS 

##  SQL Server Full Text Search

##   Notification Services

Notification Services is a platform for alerting users to changes in databases 
 Ex: Mail, SMS etc

##   Distribution Transaction Co-coordinator (MSDTC)	

The Distributed Transaction Coordinator (MSDTC) is a service that manages two-phase commit transactions spanned over multiple servers. This service ensures that **changes that need to be made to data stored on different servers complete successfully.** 

##   Database Mail



## System Databases

```sql
use Master
go

create database MayBatch
go
```

## OLTP and OLAP

OLTP and OLAP: The two terms look similar but refer to different kinds of systems. Online transaction processing (OLTP) captures, stores, and processes data from transactions in real time. Online analytical processing (OLAP) uses complex queries to analyze aggregated historical data from OLTP systems.

### What is OLTP?

An OLTP system captures and maintains transaction data in a database. Each transaction involves individual database records made up of multiple fields or columns. Examples include banking and credit card activity or retail checkout scanning.

In OLTP, the emphasis is on fast processing, because OLTP databases are read, written, and updated frequently. If a transaction fails, built-in system logic ensures data integrity.

### What is OLAP?

OLAP applies complex queries to large amounts of historical data, aggregated from OLTP databases and other sources, for data mining, analytics, and [business intelligence](https://www.stitchdata.com/resources/business-intelligence-tools/) projects. In OLAP, the emphasis is on response time to these complex queries. Each query involves one or more columns of data aggregated from many rows. Examples include year-over-year financial performance or marketing lead generation trends. OLAP databases and [data warehouses](http://www.stitchdata.com/resources/data-warehouse/) give analysts and decision-makers the ability to use custom reporting tools to turn data into information. Query failure in OLAP does not interrupt or delay transaction processing for customers, but it can delay or impact the accuracy of business intelligence insights.

### ETL: the force that joins OLTP and OLAP

The data from one or more OLTP databases is ingested into OLAP systems through a process called [extract, transform, load (ETL)](https://www.stitchdata.com/etldatabase/etl-process/). With an ETL tool, users can collect data from several [sources](https://www.stitchdata.com/integrations/sources/) and send it to a [destination](https://www.stitchdata.com/integrations/destinations/), such as an OLAP data warehouse, where it is queried by [analytics and business intelligence tools](https://www.stitchdata.com/integrations/analysis-tools/) for insights.



### OLTP vs. OLAP: side-by-side comparison

OLTP is operational, while OLAP is informational. A glance at the key features of both kinds of processing illustrates their fundamental differences, and how they work together.

|                         | OLTP                                                         | OLAP                                                         |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Characteristics**     | Handles a large number of small transactions                 | Handles large volumes of data with complex queries           |
| **Query types**         | Simple standardized queries                                  | Complex queries                                              |
| **Operations**          | Based on INSERT, UPDATE, DELETE commands                     | Based on SELECT commands to aggregate data for reporting     |
| **Response time**       | Milliseconds                                                 | Seconds, minutes, or hours depending on the amount of data to process |
| **Design**              | Industry-specific, such as retail, manufacturing, or banking | Subject-specific, such as sales, inventory, or marketing     |
| **Source**              | Transactions                                                 | Aggregated data from transactions                            |
| **Purpose**             | Control and run essential business operations in real time   | Plan, solve problems, support decisions, discover hidden insights |
| **Data updates**        | Short, fast updates initiated by user                        | Data periodically refreshed with scheduled, long-running batch jobs |
| **Space requirements**  | Generally small if historical data is archived               | Generally large due to aggregating large datasets            |
| **Backup and recovery** | Regular backups required to ensure business continuity and meet legal and governance requirements | Lost data can be reloaded from OLTP database as needed in lieu of regular backups |
| **Productivity**        | Increases productivity of end users                          | Increases productivity of business managers, data analysts, and executives |
| **Data view**           | Lists day-to-day business transactions                       | Multi-dimensional view of enterprise data                    |
| **User examples**       | Customer-facing personnel, clerks, online shoppers           | Knowledge workers such as data analysts, business analysts, and executives |
| **Database design**     | Normalized databases for efficiency                          | Denormalized databases for analysis                          |



OLTP provides an immediate record of current business activity, while OLAP generates and validates insights from that data as it’s compiled over time. That historical perspective empowers accurate forecasting, but as with all business intelligence, the insights generated with OLAP are only as good as the data pipeline from which they emanate.

### Stitch optimizes the data pipeline

To get actionable intelligence from OLTP data, it must be extracted, transformed, and loaded into a data warehouse for analysis. While this can be done with in-house programming resources, [data ingestion](https://www.stitchdata.com/resources/data-ingestion/) is more effectively handled with an ETL tool. ETL tools remove the need for constant code maintenance due to changing data source APIs, reporting requirements, and business needs. An ETL tool like Stitch optimizes OLTP data ingestion, freeing up time and IT staff to focus on more value-added activities.

Simplify the process of pulling OLTP source data into your warehouse for OLAP. Choose a solution that scales with your data and provides the support you need to stay ahead of changes and on track for insights.

Stitch is designed to make the process of populating your data warehouse simple and easy. [Try Stitch today](https://www.stitchdata.com/signup/) to close the gap between OLTP and OLAP. It’s free to try and setup takes minutes.

## 

![](E:\github_repos\pajarnas.github.io\themes\butterfly\source\img\微信图片_20210505004937.png)

# SQL Server Tools

## SQL Server Configuration Manager

You can manage SQL Server services and connection configurations by navigating objects in the Console tree 

## SQL Server Management Studio 

Microsoft SQL Server Management Studio, new in Microsoft SQL Server, is an integrated environment for **accessing, configuring, managing, administering, and developing all components of SQL Server.** 

SQL Server Management Studio combines the features of Enterprise Manager, Query Analyzer, and Analysis Manager, included in previous releases of SQL Server, into a single environment. In addition, SQL Server Management Studio works with all components of SQL Server such as Reporting Services, Integration Services, SQL Server Compact Edition, and Notification Services. Developers get a familiar experience, and database administrators get a single comprehensive utility that combines easy-to-use graphical tools with rich scripting capabilities 

## SQL Server Profiler

SQL Server Books Online (BOL)

SQLCMD

SQLCMD Utility : SQLCMD uses OLE DB to execute Transact-SQL batches, while Management Studio uses .NET SqlClient. This difference sometimes leads to different behavior when the same scripts are executed in them. 

#  SQL Server 

Microsoft SQL Server database is a collection of objects that hold and manipulate data 

properties and features 

-  It is a collection of **many objects, such as tables, views, stored procedures, and constraints**.
-  It is owned by **a single SQL Server login account .**
-  It maintains its own **set of user accounts, roles, schemas, and security .**
-  It has its own set of system tables and views to hold the database catalog .
-  It has its own transaction log and manages its own transactions.
-  It can range in size from 1 megabyte (MB) to a technical limit of 1,048,516 terabytes .
-  It can grow and shrink, either automatically or by command.
-  It can have objects joined in queries with objects from other databases in the same SQL Server instance or on linked servers.  

## SQL Server instance

or Database Engine Instance, is a complete SQL server and you can install many instances on a machine but you can have only 1 default instance. An SQL Server instance has its own copy of the server files, databases and security credentials. ... Each instance manages several system databases and one or more user databases.

**An instance of the Database Engine is a copy of the sqlservr.exe executable that runs as an operating system service**. Each instance manages several system databases and one or more user databases. Each computer can run multiple instances of the Database Engine. Applications connect to the instance in order to perform work in a database managed by the instance.

## System Databases

A new SQL Server installation always includes four databases 

### master

The master database is composed of system tables that **keep track of the server installation as a whole and all other databases that are subsequently created**. Although every database has a set of system catalogs that maintain information about objects it contains, the master database has system catalogs that keep information about disk space, file allocations and usage, systemwide configuration settings, endpoints, login accounts, databases on the current instance, and the existence of other SQL servers (for distributed operations).

The master database is **critical to your system**, so always keep a current **backup copy** of it. **Operations** such as creating another database, changing configuration values, and modifying login accounts **all make modifications to master,** so after performing such actions, you should back up master

### model 

The model database is simply **a template database.** <u>Every time you create a new database, SQL Server makes a copy of model to form the basis of the new database.</u> If you’d like every new database to start out with certain objects or permissions, you can put them in model, and all new databases will inherit them. You can also change most properties of the model database by using the ALTER DATABASE command, and those property values will then be used by any new database you create.

### tempdb 

The tempdb database **is used as a workspace.** It is **unique among SQL Server databases because it’s re-created–not recovered–every time SQL Server is restarted.** It’s used for temporary tables explicitly created by users, for worktables that will hold intermediate results created internally by SQL Server during query processing and sorting, for maintaining row versions used in

The tempdb database sizing and configuration is critical for optimal functioning and performance of SQL Server. 

### mssql system resource (hidden)

### msdb 

The msdb database **is used by the SQL Server Agent service,** which performs scheduled activities such as backups and replication tasks, and the Service Broker, which provides queuing and reliable messaging for SQL Server. 

**When you are not performing backups and maintenance on this database, you should generally ignore msdb.** 

All the information in msdb is accessible from Object Explorer in SQL Server Management Studio, so you usually don’t need to access the tables in this database directly. You can think of the msdb tables as another form of system tables

## User Databases

User databases are created by users (Administrators, developers, and testers who have access to create databases).

## Database Files

A database file is nothing more than an **operating system file**. (In addition to database files)

**Primary data files**:  Every database has one primary data file that **keeps track of all the rest of the files in the database**, in addition to storing data. By convention, **a primary data file has the extension .mdf.** 

**Secondary data files**: A database can have zero or more secondary data files. By convention**, a secondary data file has the extension .ndf.**

**Log files**: Every database has a**t least one log file that contains the information necessary to recover all transactions in a database**. By convention, a log file has the extension **.ldf.** 

## Tasks (Jobs)

What is a SQL Job? A job is a specified series of **actions** that **SQL Server Agent performs**. Use jobs to define an **administrative task** that can be run one or more times and **monitored for success or failure**. A job can run on one **local server or on multiple remote servers**. Some examples of SQL Jobs are automatic weekly backup, sending auto emails, newsletters, writing log files, and audit logs. 

# The Transact-SQL Programming Language

Transact-SQL (T-SQL) is **an extension to SQL** developed by Microsoft and Sybase.

T-SQL is the **programming language** for the **commands** used to **administer SQL Server**, create and manage **objects** in a physical or virtual **instance of SQL Server**, as well as to insert, retrieve, modify and delete **data** in **SQL Server tables**.

The **SQL standards** published by the International Standards Organization (**ISO**) and the American National Standards Institute (**ANSI**) defined a software language, and Transact-SQL was developed and extended from this definition.

T-SQL **extends** the SQL standard to include **procedural programming**, **local variables**, **support functions for string processing**, **data processing**, **math and so forth**, as well as modifications to **DELETE and UPDATE statements**.

SQL is a standard interactive and programming language **for querying and modifying data and managing databases**. Although SQL is both an ANSI and an ISO standard, many database products support SQL with proprietary extensions to the standard language 

Transact-SQL is **central to using SQL Server**. All applications that communicate with an instance of SQL Server do so by sending Transact-SQL statements to the server, regardless of the user interface of the application 

the following applications use T-SQL to communicate with SQL Server:

1. General office applications;

2. Applications using a **graphical user interface** to select the tables and columns to view data from;

3. Applications that use general language sentences to define the data a user wants to view;

4. Business applications that store data in SQL Server databases;

5. Transact-SQL scripts that are run by utilities like sqlcmd;

6. Applications created with development systems including Microsoft Visual C++, Microsoft Visual Basic, or Microsoft Visual J++ that use database APIs such as ADO, OLE DB, and ODBC;

7. **Web pages** that extract data from SQL Server databases;

8. Distributed database systems where SQL Server is replicated to various databases or distributed queries are executed;

9. Data warehouses in which data is taken from online transaction processing systems and synopsized for decision-support analysis.

he **sqlcmd** utility lets you enter Transact-SQL statements, system procedures, and script files through a variety of available modes:

- At the command prompt.
- In **Query Editor** in SQLCMD mode.
- In a Windows script file.
- In an operating system (Cmd.exe) job step of a SQL Server Agent job.

| **Source**        | **Common** **Name** | **Full Name**                                            |
| ----------------- | ------------------- | -------------------------------------------------------- |
| ANSl/lSO Standard | SQL/PSM             | SQL/Persistent Store Module                              |
| IBM               | SQL PL              | SQL Procedural Language                                  |
| Microsoft/Sybase  | T-SQL               | Transact-SQL                                             |
| MYSQL             | MYSQL               | MYSQL                                                    |
| Oracle            | PL/SQL              | Procedural language/SQL                                  |
| PostgreSQL        | PL/SQL              | Procedural Language/PostgreSQL Structured Query Language |

## Types of Transact-SQL Statements

There are three basic types of T-SQL statements: DML, DDL, and DCL.

**DML**. That's **data manipulation** language. These are the main language statements that you'll use and are about getting data into and out of tables. They include reading data by using SELECT, and modifying it by INSERT, UPDATE, DELETE, and MERGE.

**DDL** statement. That's **data definition** language. These are used to define how data is stored. For example, you might need to create a new table to hold data. They include words like CREATE, ALTER, and DROP.

**DCL** statement. That's **data control** language. These statements are used to say who is able to access the data in the first place. They include words like GRANT, DENY, and REVOKE.

## Transact-SQL Syntax Elements

| Convention        | Used for                                                     |
| :---------------- | :----------------------------------------------------------- |
| UPPERCASE         | Transact-SQL **keywords**.                                   |
| *italic*          | **User-supplied parameters** of Transact-SQL syntax.         |
| **bold**          | Type **database names**, **table** names, **column** names, **index** names, stored procedures, utilities, data type names, and text exactly as shown. |
| underline         | Indicates the **default value applied** when the clause that contains the underlined value is omitted from the statement. |
| \| (vertical bar) | Separates syntax items enclosed in brackets or braces. You can use only one of the items. |
| `[ ]` (brackets)  | **Optional syntax items**. Don't type the brackets.          |
| { } (braces)      | **Required syntax items**. Don't type the braces.            |
| [**,**...*n*]     | Indicates the preceding item can be repeated *n* number of times. The occurrences are separated by commas. |
| [...*n*]          | Indicates the preceding item can be **repeated *n* number of times**. The occurrences are separated by blanks. |
| ;                 | Transact-SQL statement terminator. Although the semicolon isn't required for most statements in this version of SQL Server, it will be required in a future version. |
| <label> ::=       | The name for a block of syntax. Use this convention to group and label sections of lengthy syntax or a unit of syntax that you can use in more than one location within a statement. Each location in which the block of syntax could be used is indicated with the label enclosed in chevrons: <label>.  A set is a collection of expressions, for example <grouping set>; and a list is a collection of sets, for example <composite element list>. |
| Batch Derative    |                                                              |



## Where Clause

### Using Wildcards with LIKE 

| **Wildcard** | **Usage**                                                    |
| ------------ | ------------------------------------------------------------ |
| %            | Represents  a string of zero or more characters.             |
| _            | Represents  a single character.                              |
| [ ]          | Specifies  a single character, from a selected range or list. |
| [ ^  ]       | Specifies  a single character not within the specified range |

### Negating a Search Condition 

 The NOT logical operator, unlike AND and OR, isn’t used to combine search conditions, but instead is used to negate the expression that follows it. 

You can use multiple operators (AND, OR, NOT) in a single WHERE clause, but it is important to keep your intentions clear by properly **embedding your ANDs and ORs in parentheses**.

**The AND operator limits the result set, and the OR operator expands the conditions for which rows will be returned.** When multiple operators are used in the same WHERE clause, operator precedence is used to determine how the search conditions are evaluated. 

•For example, **the NOT operator takes precedence (is evaluated first) before AND. The AND operator takes precedence over the OR operator**. **Using both AND and OR operators in the same WHERE clause without using parentheses can return unexpected results** 

### Using BETWEEN for Date Range Searches 

### Use of In Operator

## Batch Directives

SQL Server processes single or multiple Transact-SQL statements in batches. A batch directive instructs SQL Server to parse and execute all of the instructions within the batch. There are two basic methods for handing off batches to SQL Server.

**GO** : SQL Server utilities interpret GO as a signal to send the current batch of Transact-SQL statements to SQL Server. A GO command delineates batches of Transact-SQL statements to tools and utilities and ends the batch. A GO command is not an actual Transact-SQL statement.

**EXEC** :The EXEC directive is used to execute a user-defined function, system procedure, user-defined stored procedure, or an extended stored procedure; it can also control the execution of a character string within a Transact-SQL batch. Parameters can be passed as arguments, and a return status can be assigned.

## Identifiers

### Standard Identifiers: 

 Standard identifiers can contain from one to 128 characters, including letters,

 symbols (_, @, or #), and numbers. No embedded spaces are allowed in

 standard identifiers.

 The first character must be an alphabetic character of a-z or A-Z.

 After the first character, identifiers can include letters, numerals, or the @,

 $, #, or _ symbol

### Identifier names starting with a symbol have special uses:

 An identifier beginning with the @ symbol denotes a local variable

 or parameter.

  An identifier beginning with a number sign (#) denotes a temporary

 table or procedure.

  An identifier beginning with a double number sign (##) denotes a global temporary object.

### Delimited Identifiers

 If an identifier complies with all of the rules for the format of identifiers, it can be used with or without delimiters. If an identifier does not comply with one or more of the rules for the format of identifiers, it must always be delimited

### Delimited identifiers can be used in the following situations:

When names contain embedded spaces

When reserved words are used for object names or portions of object names

## Coding style

```sql

/* =========================================
Object: Day 1 Assignment 
Author: Saige Zhang
Create date: May 4, 2021
Description: SQL: Comprehensive practice
============================================ */

SELECT
    T1.col1,
    T1.col2,
    T2.col3
FROM
    table1 T1
    INNER JOIN ON Table2 T2 ON T1.ID = T2.ID
WHERE
    T1.col1 = 'xxx'
    AND T2.Col3 = 'yyy'
    
    
```

- capitalize reserved words
- main keywords on new line
- can't get used to commas before columns
- always use short meaningful table aliases
- prefix views with v
- prefix stored procs with sp (however don't use "sp_" which is reserved for built in procs)
- don't prefix tables
- table names singular

Select

> ```sql
> CREATE PROC [dbo].[procTable_SEL]
> AS
> SET NOCOUNT ON
> SELECT
>     [Column1] = T1.[col1]
>   , [Column2] = T1.[col2]
>   , [Column3] = T2.[col3]
> FROM [dbo].[Table] T1    
> INNER JOIN ON [dbo].[Table2] T2 ON T1.ID = T2.ID
> WHERE
>       T1.[col1] = 'xxx'
>   AND T2.[Col3] = 'yyy'
> SET NOCOUNT OFF
> GO
> ```

------

Update

> ```sql
> CREATE PROC [dbo].[procTable_UPD]
> AS
> SET NOCOUNT ON
> UPDATE t1 SET
>     [Column1] = @Value1
>   , [Column2] = @Value2
>   , [Column3] = @Value3
> FROM [dbo].[Table1] T1
> INNER JOIN ON [dbo].[Table2] T2 ON T1.[ID] = T2.[ID]
> WHERE
>       T1.[col1] = 'xxx'
>   AND T2.[Col3] = 'yyy'
> SET NOCOUNT OFF
> GO
> ```

------

Insert

> ```sql
> CREATE PROC [dbo].[procTable_INS]
> AS
> SET NOCOUNT ON
> INSERT INTO [Table1] (
> [Column1]
>   , [Column2]
>   , [Column3]
> )
> VALUES (
>     @Value1
>   , @Value2
>   , @Value3
> )
> SET NOCOUNT OFF
> GO
> ```

OR

> ```sql
> CREATE PROC dbo.procTable_INS
> AS
> SET NOCOUNT ON
> INSERT INTO [table1] (
>     [Column1]
>   , [Column2]
>   , [Column3]
> )
> SELECT
>     [Column1] = T1.col1
>   , [Column2] = T1.col2
>   , [Column3] = T2.col3
> FROM dbo.Table1 T1    
> INNER JOIN ON Table2 T2 ON T1.ID = T2.ID
> WHERE
>       T1.[col1] = 'xxx'
>   AND T2.[Col3] = 'yyy'
> SET NOCOUNT OFF
> GO
> ```

------

Delete

> ```sql
> CREATE PROC dbo.procTable_DEL
> AS
> SET NOCOUNT ON
> DELETE
> FROM [dbo].[Table1] T1
> INNER JOIN ON [dbo].[Table2] T2 ON T1.[ID] = T2.[ID]
> WHERE
>       T1.[col1] = 'xxx'
>   AND T2.[Col3] = 'yyy'
> SET NOCOUNT OFF
> GO
> ```

## Data Types

![](E:\github_repos\pajarnas.github.io\themes\butterfly\source\img\image-20210505012035271.png)

# Retrieving Data

## Result set 

## Syntax

<> : 

city = or,or,or  | city in('London','Paris')

## void difference

null, 0, ''; 

select 8+null the result set is null. 

![image-20210504103537917](C:\Users\saige\AppData\Roaming\Typora\typora-user-images\image-20210504103537917.png)



![image-20210504103608354](C:\Users\saige\AppData\Roaming\Typora\typora-user-images\image-20210504103608354.png)

![image-20210504103644029](C:\Users\saige\AppData\Roaming\Typora\typora-user-images\image-20210504103644029.png)

![image-20210504103857816](C:\Users\saige\AppData\Roaming\Typora\typora-user-images\image-20210504103857816.png)

```sql
Select ContactName, City, Country from Customers 
order by Country,City asc

Select ContactName, City, Country from Customers 
order by Country,City desc

-- 
this is a comment
--
```

## indentifier

letter, symbol, number, no space

![image-20210504104653773](C:\Users\saige\AppData\Roaming\Typora\typora-user-images\image-20210504104653773.png)

use bracts to include a space

```
declare @x int
set @x = 2
if @x%2=0
    begin
	print 'even'
	select * from Employees where EmployeeID = @x
	end
else
	print 'odd'
```



## **Case**

![image-20210504105038766](C:\Users\saige\AppData\Roaming\Typora\typora-user-images\image-20210504105038766.png)

```sql
Select Title, TitleOfCourtesy, case TitleOfCourtesy 
		When 'Mr.' then 'Male'
		when 'Mrs.' then 'Femaile'
		else 'Others' 
		END
		as 'gender'
from Employees
```