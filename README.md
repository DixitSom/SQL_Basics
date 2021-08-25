# SQL

## Table of Content

* Introduction
* Syntax
  * Select
  * Where
  * Order by
  * Null values
  * Select Top
  * Aggregate Functions
  * Like
  * In and Between
  * SQL Joins
  * Group By
  * Having
  * Order Of Execution
* Other Queries
  * Insert Into
  * Update
  * Delete
* SQL Database
  * Create Database
  * Drop Database
  * Create Table
  * Drop Table
  * Alter Table
* Concepts of Database
  * Primary Key
  * Foreign Key
  * ACID properties
  * CAP Theorem
  * Normalization
  * Indexes
  * Transactions
  * Locking Mechanism
  * Database Isolation Levels
  * Triggers

***

## Intoduction

Structured Query Language is a standard Database language that used to update, insert and retrive information from relational Databases.

SQL is used when you have structured data in your table. It is not used on the database which do not have a fixed structured tabular data. Those called No-SQL Databases.

Like MongoDB etc.

***

## Syntax

In this section we will learn about various queries that we can perform on SQL Database.

Before that I would like to show you demo database that we will use to understand these queries.



### Select

This statement is used to access data from the table.

__Syntax__

```
SELECT col1, col2, .. FROM table_name;
```
It will return the specified columns values from the table.

If you want to get information about all the columns then you can run.

```
SELECT * FROM table_name;
```

Columns may contain duplicate values so you want list of different values of column then you can run

```
SELECT DISTINCT col1, col2 .. FROM table_name;
```
***

### Where

It is used to filter the results based on condition. If you only want result that follows a certain criteria then you can use *where* clause.

__Syntax__

```
SELECT col1, col2, .. FROM table_name WHERE condition;
```

Suppose we have a table named brands.

Id | Brand | Price
-- | ----- | -----
1 | Apple | 150000
2 | Microsoft | 70000
3 | Google | 80000
4 | Facebook | 75000
5 | Tesla | 200000

Now we want all brands name which have price greater than 80000.

```
SELECT name FROM brands WHERE price > 80000;
```

Result will be.

```
Id | Brand | Price
-- | ----- | -----
1  | Apple | 150000
5  | Tesla | 200000
```

We can use *AND*, *OR* to combine two or more conditions like this.

```
SELECT col1, col2 .. FROM table_name WHERE condition1 AND condtion2 AND condition3 ...;

```
Or

```
SELECT col1, col2 .. FROM table_name WHERE condition1 OR condtion2 OR condition3 ...;
```

We can also use *NOT* operator which gives result such rows those negates the condition.

```
SELECT col1, col2 .. FROM table_name WHERE NOT condition;
```

***

### Order By

It is used to sort the results. We can sort the results using columns.

__Syntax__

```
SELECT col1, col2, .. FROM table_name
ORDER BY col1, col2 ... ASC/DESC;
```

Results will be sorted based on the values of columns.

For table

Id | Brand | Price
-- | ----- | -----
1 | Apple | 150000
2 | Microsoft | 70000
3 | Google | 80000
4 | Facebook | 75000
5 | Tesla | 200000

Lets sort the results by price.

```
SELECT * FROM brands ORDER BY price;
```

Results will be

Id | Brand | Price
-- | ----- | -----
2 | Microsoft | 70000
4 | Facebook | 75000
3 | Google | 80000
1 | Apple | 150000
5 | Tesla | 200000

By default results will be in ascending order.

***

### NULL values

In a table it might be possible if there are some null values. 

We can handle these values by using a ```IS NULL``` adn ```IS NOT NULL```.


__Syntax__
```
SELECT col1, col2, ... FROM table_name
WHERE column_name IS NOT NULL;
```

Above statement can be used to find the rows which doesn't have NULL value in specified column.

If we want to access rows that have null values for a specific columns then we can do this.

```
SELECT * FROM table_name
WHERE column_name IS NULL;
```

***

### Select Top

Using Top we can select top elements from a result-set.

__Syntax__
```
SELECT TOP number/percent column(s) FROM table_name
WEHRE condition;
```

we will only get top n result rows from result-set.

### Aggregate Functions
Aggregate function are very usefull in queries. They can help to get information very quickly.

Following are some aggregate functions.
* Min
* Max
* Count
* Sum
* Avg

1. __Min__:- This is used to get the minimum from a column.

   __Syntax__
   ```
   SELECT MIN(column_name) FROM table_name WHERE condition;
   ```
2. __Max__:- It used to find the maximum from the column
   
   __Syntax__
   ```
   SELECT MAX(column_name) FROM table_name WHERE condition;
   ```
3. __Count__:- It is used to count the number of entries for a specific column or result-set.
   
   __Syntax__
   ```
   SELECT COUNT(column_name) FROM table_name WHERE condition;
   ```
4. __Sum__:- It will give the sum of all values from a column result-set.
   
   __Syntax__
   ```
   SELECT SUM(column_name) FROM table_name WHERE condition;
   ```
5. __Avg__:- It gives the average of all result-set values for a column.
   
   __Syntax__
   ```
   SELECT AVG(column_name) FROM table_name WHERE condition;
   ```

***

### Like

This is used for pattern matching in string type attributes.

__Syntax__
```
SELECT * FROM table_name
WHERE column_name LIKE "sample_string";
```

It does a case insentive matching.

Mostly *LIKE* statement are used with wildcards

These are following wildcards.

Symbol | Description | Example | Syntax
------ | ----------- | ------- | ------
% | Represents zero or more characters | bl% finds bl, black, blue, and blob | ```SELECT * FROM table_name WHERE column_name LIKE '%anything%'```
_ | Represents a single character | h_t finds hot, hat, and hit | ```SELECT * FROM table_name WHERE column_name LIKE 'any_'```
[] | Represents any single character within the brackets | h[oa]t finds hot and hat, but not hit | ```SELECT * FROM table_name WHERE column_name LIKE 'h[oa]t'```
^ | Represents any character not in the brackets | h[^oa]t finds hit, but not hot and hat | ```SELECT * FROM table_name WHERE column_name LIKE 'h[^oa]t'```
 \- | Represents a range of characters | c[a-b]t finds cat and cbt | ```SELECT * FROM table_name WHERE column_name LIKE 'c[a-b]t'```

***

### In and Between

In operator is used when you want to check for multiple values for a attribute.

__Syntax__
```
SELECT col1, col2, .. FROM table_name WHERE column_name IN (value1, value2, ...);
```

Between is used to specify a value range for column.

__Syntax__
```
SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;
```

***

### SQL Joins

Joins are used to combine data or rows from multiple tables.

There are four types of joins
1. Inner Join
2. Left Join
3. Right Join
4. Full Join
   
__Inner Join__:- It select rows which have matching values in both the table.

__Syntax__
```
SELECT t1.col1, t1.col2, .. , t2.col1, t2.col2, .. FROM table1 AS t1 INNER JOIN table2 AS t2 ON t1.column_name = t2.column_name WHERE condition;
```

__Left Join__:- It will keep all the entries for first or left table and will only keep rows from second table that have a matching value for specified attribute.

__Syntax__:
```
SELECT t1.col1, t1.col2, .. , t2.col1, t2.col2, .. FROM table1 AS t1 LEFT JOIN table2 AS t2 ON t1.column_name = t2.column_name WHERE condition;
```

__Right Join__:- It will keep all the entries for second or right table and will only keep rows from first table that have a matching value for specified attribute.

__Syntax__:
```
SELECT t1.col1, t1.col2, .. , t2.col1, t2.col2, .. FROM table1 AS t1 RIGHT JOIN table2 AS t2 ON t1.column_name = t2.column_name WHERE condition;
```

__Full Join__:- It will return all rows when there is a match in left table or right table.

__Syntax__:
```
SELECT t1.col1, t1.col2, .. , t2.col1, t2.col2, .. FROM table1 AS t1 FULL JOIN table2 AS t2 ON t1.column_name = t2.column_name WHERE condition;
```

__Note__:- Self join are used to take any of above joins with itself.

***

### Group By

This statement is used to group the rows from result set based on common values of attributes

__Syntax__:
```
SELECT column_name(s) FROM table_name
WHERE condition
GROUP BY column_name(s);
```

Group By often used with aggregate functions like this.

```
SELECT SUM(col1), MAX(col1), MIN(col2), ... FROM table_name
WHERE condition
GROUP BY column_name(s);
```
***

### Having

It is also used as similar to where clause to filter the results.

*HAVING* Clause also often used with *GROUP BY* statements. *HAVING* clause added to the SQL beacuse WHERE can not be used with aggregate functions

__Syntax__:
```
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition;
```

### Order Of Execution

Lets see this is an complete query.

```
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```
Order Of execution will be.

```
FROM AND JOINS > WHERE > GROUP BY > HAVING > SELECT > DISTINCT > ORDER BY > LIMIT/OFFSET 
```

You need to keep this order in mind to have better understanding of query execution.

***

## Other Queries

### Insert into
 This statement is used to insert new rows or records into table

 __Syntax__:
```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

It can also be done as 

```
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

But make sure you have order of values according to attributes order in table.

***

### Update

This statement is used to modify existing row or record in the table

 __Syntax__:
```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

__Note__:- Be carefull when using this statement and keep an eye over *WHERE* clause and condtion beacause if you ommit *WHERE* it will update all the rows in the table.

***

### Delete

It is used to delete the records from table.

 __Syntax__:
```
DELETE FROM table_name WHERE condition;
```

To delete all records we can ommit *where* clause.

```
DELETE FROM table_name;
```



***

## SQL Database

These are some queries used to define schema in database

### Create Database

This statement is used to create a new database in DBMS.

 __Syntax__:
```
CREATE DATABASE db_name;
```

***

### Drop Database

It is used to drop or remove an existing database from DBMS.

__Syntax__
```
DROP DATABASE db_name;
```

***

### Create Table

It is used to create table in the database.

 __Syntax__:
```
CREATE TABLE table_name(
    col1 <datatype> <constraints> DEFAULT <default>,
    col2 <datatype> <constraints> DEFAULT <default>,
    ...
);
```
__Note__:- Datatype information is compulsory when executing this statement.
All other are optional.

Example.
```
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) 
);
```

*IF NOT EXIST* is also used to check if a table with the same name exist in databse or not.

```
CREATE TABLE Persons IF NOT EXISTS (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) 
);
```

***

### Drop Table

This statement is used to drop or remove a table from database.

__Syntax__
```
DROP TABLE table_name;
```

***

### Alter Table

This statement is used to modify the definition or schema of an existing table.

It can be used to add or remove columns from table and also can be used to modify constraintes of a column in a table.

__Add Column Syntax__
```
ALTER TABLE table_name
ADD column_name datatype;
```

__Remove Column Syntax__
```
ALTER TABLE table_name
DROP COLUMN column_name;
```

__Modify Column Syntax__
```
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

***

Read [more](https://www.w3schools.com/sql/default.asp).

## Concepts of Database

***

### Primary Key
Primary key is the minimul set of attributes which can Uniquely Identify the row(tuple). It is used to fetch a unique record from database.

***

### Foreign Key

Foreign key is the key that is primary key to another table and it acts as an cross-reference between tables. Foreign Key provides a link between data in two tables.

***

### ACID Properties

To Maintain consistency in database, before and after the transaction, these properties are followed which called ACID properties

* Atomicity
  
  It is all or Nothing rule. It means a transaction can not be executed partially. Either it will completely execute or None of it.
* Consistency
  
  It refers to the correctness of database. Integrity constraints must be maintained so that database is consistent before and after the execution of transaction.

* Isolation
  
  This is the property to execute two or more transaction concurrently without interfering each other. Output or changes made by one transaction will only be visible to any other transaction after its complete execution.

* Durability
  
  Durability means if a transaction occure then changes made by this transaction should be permanent and persisent it should not lost even if system fails.

You can understand these concepts in a lot more details from [here](https://www.geeksforgeeks.org/acid-properties-in-dbms/).
  
***

### CAP Theorem 

CAP theorem is depend on three factors those are.
  * __Consistency__:- Database should be consistent for all read and write operations.
  * __Availability__:- Data should be available for all read operations.
  * __Partition tolerance__:- System should be tolerant towards system failures like it should work somehow.
  
CAP theorem states that if there is a network failure then there is a tradeoff between *Consistency* and *Availability*.

If there is high consistency then availability becomes less and viceversa.

Read [more](https://www.bmc.com/blogs/cap-theorem/#).

***

### Normalization

Database Normalization is the process of eliminate data redundancy from database. We organize attributes in such a way so that redundacy in data get reduced.
*Normal forms* are used to reduce data redundancy.

  1. __First Normal Form__:- If there are no multivalues attributes then database is in First Normal Form.
  2. __Second Normal Form__:- If a relation is in *First Normal Form* and it does not have any paritial dependencies.
        
        __Partial Dependency__:- If a subset of a Candidate Key determines non-prime attribute, it is called partial dependency.

  3. __Third Normal Form__:- If a relation is in *Second Normal Form* and does not have any __transitive dependency__ then it database is in its Third Normal Form.

      __Transitive Dependency__:- If A->B and B-> C are two functional dependecies then dependency A-> C is called transitive dependency.
   
  4. __BCNF__:- If a relation is in *Third Normal Form* and for every functional dependency LHS is a super key. Then relation will be in BCNF.

Read [more.](https://www.geeksforgeeks.org/normal-forms-in-dbms/)

***

### Indexing

Indexing in database is way to optimize the performance of database. it is a data structure technique used to access data in faster way.

Read [more.](https://www.geeksforgeeks.org/indexing-in-databases-set-1/)

***

### Transactions

Transaction is group of task which acts as unit task. Tasks in the transaction are united so that either all of them executed or none are.

If any single task fails, complete transactions fails. In transaction partial execution is not possible.

Read [more](https://www.geeksforgeeks.org/sql-transactions/).

***

### Locking Mechanism

Locking mechanism in database is required for concurrency control. Database should follow *Isolation* property, that is one transcation can not perform any operation on attributes which are already accessed by any other transaction.

In order to achive that locking mechanism is impletemented so that transaction can lock attributes while executing or accessing them.

Read [more](https://www.geeksforgeeks.org/implementation-of-locking-in-dbms/).

***

### Database Isolation Levels

*Level of Isolation* means the degree of isolation by which transaction are isolated.

These are following four levels of Isolation.

1. __Read Uncommited__:- It is the lowest level of isolation. It allows dirty read in transaction.
2. __Read Commited__:- It does not allow dirty read in transaction. Transaction holds a read or write lock on current row, and prevent other transaction to read and write from row.
3. __Repeatable Read__:- It prevents non-repeateble reads by locking all rows from which it is reading as well as rows in which it is writing or updating something.
4. __Serialiable__:- It is the highest level of isolation. In this transaction that are executing concurrently, seems to execute serially.

Read [more](https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/).

***

### Triggers

Trigger is a stored procedure in database which automatically invokes when a particular event happens.

Syntax:
```
create trigger [trigger_name] 
[before | after]  
{insert | update | delete}  
on [table_name]  
[for each row]  
[trigger_body] 
```

Read [more](https://www.geeksforgeeks.org/sql-trigger-student-database/).

***

## References
* https://www.geeksforgeeks.org/acid-properties-in-dbms/
* https://www.bmc.com/blogs/cap-theorem/#
* https://www.geeksforgeeks.org/normal-forms-in-dbms/
* https://www.geeksforgeeks.org/indexing-in-databases-set-1/
* https://www.geeksforgeeks.org/sql-transactions/
* https://www.geeksforgeeks.org/implementation-of-locking-in-dbms/
* https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/
* https://www.w3schools.com/sql/
* https://www.w3schools.com/sql/default.asp
