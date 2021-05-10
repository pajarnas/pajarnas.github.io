---

title: SEP I: MS SQL Server Installation and Basic Knowledge
date: 05/03/2021
updated: 
tags: 
  - notes
  - SEP
  - Full-Stack
  - MSSQLSERVER
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

# SQL Server Replication

Replication is a set of technologies for **copying and distributing data and database objects from one database to another** and then synchronizing between databases to maintain consistency. 

# SQL Server Account

| Service                    | Account Name              |
| -------------------------- | ------------------------- |
| SQL Server Agent           | NT Service\SQLAgent$ANTRA |
| SQL Server Database Engine | NT Service\MSSQL$ANTRA    |
| SQL Server Browser         | NT AUTHORITY\LOCALSERVICE |



NT_AUTHORITY essentially refers to the Windows operating system itself. Or perhaps as "things the OS authorizes on your behalf."

(NT meant New Technology, a version of the OS generally meant for businesses. )

The "**NT**" token is basically a legacy token left from earlier times. You can think of it as a surrogate for Windows itself. More officially, it's the parent for a set of service users that handle background tasks and maintenance operations.

The tokens on the right side of the slash refer to **individual internal service "users" of the OS**. 

For example, 

- NT AUTHORITY\SYSTEM handles system services, 
- NT AUTHORITY\LOCAL SERVICE does local services, 
- NT AUTHORITY\NETWORK SERVICE is network services, 



SQL Server Agent is a Microsoft Windows service that executes scheduled administrative tasks, which are called *jobs* in SQL Server.

# SQL Server Collation

It sets how the database server **sorts (compares pieces of text)**. in this case:

```sql
SQL_Latin1_General_CP1_CI_AS
```

breaks up into interesting parts:

1. `latin1` makes the server treat strings using charset latin 1, basically ascii
2. `CP1` stands for Code Page 1252
3. `CI` case insensitive comparisons so 'ABC' would equal 'abc'
4. `AS` accent sensitive, so 'ü' does not equal 'u'

Database Engine Configuration

## Authentication Mode

password for the SQL Server system administrator (sa) account.

Current User

SQL Server administrators have unrestricted access to the Database Engine.

Object type:

Users, Groups, or Built-in security principals

Location:

LAPTOP-S1RBCB08\saige

## Data Directories

Data root directory:

C:\Program Files\Microsoft SQL Server\

System database   directory:

C:\Program Files\Microsoft\SQL Server\MSSQL15.ANTRA\MSSQL\Data

User database directory:

C:\Program Files\Microsoft SQL Server\MSSQL15.ANTRA\MSSQL\Data

User database log directory:

C:\Program Files\Microsoft SQL Server\MSSQL15.ANTRA\MSSQL\Data

Backup directory:

C:\Program Files\Microsoft SQL Server\MSSQL15.ANTRA\MSSQL\Backup

# What is PolyBase?

PolyBase enables your SQL Server instance to query data with T-SQL directly from SQL Server, Oracle, Teradata, MongoDB, Hadoop clusters, Cosmos DB without separately installing client connection software. You can also use the generic ODBC connector to connect to additional providers using third-party ODBC drivers. PolyBase allows T-SQL queries to join the data from external sources to relational tables in an instance of SQL Server.

## Why use PolyBase?

PolyBase allows you to join data from a SQL Server instance with external data. Prior to PolyBase to join data to external data sources you could either:

- Transfer half your data so that all the data was in one location.
- Query both sources of data, then write custom query logic to join and integrate the data at the client level.

PolyBase allows you to simply use Transact-SQL to join the data.

PolyBase does not require you to install additional software to your Hadoop environment. You query external data by using the same T-SQL syntax used to query a database table. The support actions implemented by PolyBase all happen transparently. The query author does not need any knowledge about the external source.

## PolyBase uses sdasasddsa as  add wechat and 

as PolyBase enables the following scenarios in SQL Server:

- **Query data stored in Hadoop from a SQL Server instance or PDW.** Users are storing data in cost-effective distributed and scalable systems, such as Hadoop. PolyBase makes it easy to query the data by using T-SQL.
- **Query data stored in Azure blob storage.** Azure blob storage is a convenient place to store data for use by Azure services. PolyBase makes it easy to access the data by using T-SQL.
- **Import data from Hadoop, Azure blob storage, or Azure Data Lake Store.** Leverage the speed of Microsoft SQL's columnstore technology and analysis capabilities by importing data from Hadoop, Azure blob storage, or Azure Data Lake Store into relational tables. There is no need for a separate ETL or import tool.
- **Export data to Hadoop, Azure blob storage, or Azure Data Lake Store.** Archive data to Hadoop, Azure blob storage, or Azure Data Lake Store to achieve cost-effective storage and keep it online for easy access.
- **Integrate with BI tools.** Use PolyBase with Microsoft's business intelligence and analysis stack, or use any third-party tools that are compatible with SQL Server.



# **What is Azure?**

At its core, Azure is a public cloud computing platform—with solutions including **Infrastructure as a Service** (IaaS), **Platform as a Service** (PaaS), and **Software as a Service** (SaaS) that can be used for services such as analytics, virtual computing, storage, networking, and much more. It can be used to replace or supplement your on-premise servers.



