# SQL Notes

## Introduction

- SQL stands for `Structured Query Language`.
- SQL is a database management system.

## RDBMS

- It stands for `Relational Database Management System`.
- Using this, we can communicate with databases.
- By doing so, we can perform CRUD operations on the database.
- examples: MySQL, PostgreSQL, Oracle, SQL Server, etc.
- It supports the usage of SQL to fetch the data from the database.
- Table/Relation is the simplest form of data storage object in R-DB.

```markdown
Q: What are CRUD Operations?
A: CRUD stands for Create, Read, Update, and Delete operations on database values.
```

| Feature           | SQL                             | MySQL                               |
|-------------------|---------------------------------|-------------------------------------|
| Stands for        | Structured Query Language       | It is an RDBMS |
| Usage             | General purpose querying language| Database management system         |
| Flexibility       | Used by various databases       | Used primarily with MySQL databases |
| Open Source       | Varies                          | Yes                                 |
| Performance       | Depends on implementation       | Generally optimized for web apps   |

## SQL

```SQL

-- To see all the databases
SHOW DATABASES;

-- To create a new database
CREATE DATABASE db_name;

-- to perform actions in a database, we need to first isntantiate the database
USE db_name;

-- To create a new table
CREATE TABLE table_name (
    column_name1 data_type,
    column_name2 data_type
)

-- To see all the tables in a database
SHOW TABLES;

-- To insert values in a table
INSERT INTO table_name VALUES (column_name_value1, column_name_value2)

-- To fetch the values from a table
SELECT column_name1, column_name2 FROM table_name -- this is used to get "selected" values
-- To fetch all the values from a table
SELECT * FROM table_name
```

### Data Types in SQL

- **INT**: For integers.
- **VARCHAR(size)**: A variable-length string.
- **CHAR(size)**: A fixed-length string.
- **TEXT**: For large amounts of text.
- **DATE**: Stores date values.
- **TIME**: Stores time values.
- **DATETIME**: Stores both date and time values.
- **FLOAT**: For floating-point numbers.
- **DOUBLE**: For double-precision floating-point numbers.
- **DECIMAL(size, d)**: For numbers with a fixed number of decimal places.
- **BLOB**: For binary data. (Majorly used to store Audio, Video, Images, etc.)
- **ENUM**: For storing enumerated values. Can only store one value at a time.
- **SET**: For storing multiple values.
- **BOOLEAN**: For storing boolean values.
- **NULL**: For storing null values.
- For **Signed** and **Unsigned** integers, you can use `TINYINT` and `UNSIGNED TINYINT` respectively. We can also do the same for `SMALLINT`, `INT` and `BIGINT`.

For all other data types, refer to [this link](https://dev.mysql.com/doc/refman/8.0/en/data-types.html) or [here](https://www.w3schools.com/sql/sql_datatypes.asp).

```markdown
Q: What is the difference between "CHAR" and "VARCHAR"?

A: "CHAR" is a fixed-length string while "VARCHAR" is a variable-length string. This means, if I am setting any column's data type as "CHAR" of size "255", this would mean that whatever the case, "255" bytes of space is always used up. Even if a data has a length of "255" bytes, it would still have "155" bytes of space left.
Whereas with "VARCHAR", we can set a "MAX" size and if any of our data is of a size lesser than that, then it would end up taking only that mch space.
```

### ADVANCED DATATYPES

- **JSON**: For storing JSON data. It is an object with key-value pairs.

#### Example

```SQL
-- Creating a table with these columns
CREATE TABLE table_name (
    id INT,
    name VARCHAR(50),
    salary FLOAT,
    age INT UNSIGNED
);

-- Inserting values into the table
INSERT INTO table_name VALUES (1, 'John', 50000.00, 30);

```

### TYPES OF COMMANDS IN SQL

- **DDL**: Data Definition Language. This is used to define a relation schema.
  - **CRERATE**: create table, DB, view, etc.
  - **ALTER**: alter table, DB, view, etc.
  - **DROP**: delete table, DB, view, etc.
  - **TRUNCATE**: delete all rows from a table.
  - **RENAME**: rename table, DB, view, etc.

- **DRL/DQL**: Data Retrieval Language or Data Query Language. Retrieves data from the database.
  - **SELECT**: select table, DB, view, etc.

- **DML**: Data Manipulation Language. Used to perform modifications on the database.
  - **INSERT**: insert into table, DB, view, etc.
  - **UPDATE**: update table, DB, view, etc.
  - **DELETE**: delete from table, DB, view, etc.

- **DCL**: Data Control Language. Used to control the access of the database.
  - **GRANT**: grant access to table, DB, view, etc.
  - **REVOKE**: revoke access to table, DB, view, etc.

- **TCL**: Transaction Control Language. Used to perform transactions on the database.
  - **COMMIT**: commit transaction.
  - **ROLLBACK**: rollback transaction.
  - **SAVEPOINT**: savepoint.
  - **START TRANSACTION**: start transaction.

### USAGE

- We can `select` required columns from a table by mentioning them.

```SQL
SELECT column_name1, column_name2 FROM table_name
````

- The order of execution is from `RIGHT` to `LEFT`

```markdown
Q: Can we use `select` without using the `FROM` keyword?
A: yes, we can, using `Dual Tables`.

Q: What are `DUAL TABLES`?
A: `DUAL` is a dummy table that is created by `MySQL`.
```

```SQL
SELECT 44 + 11 -- here, the answer will come as 55. Even though it doesn't exist.
```

- We can use `SELECT now()` to get the server time.

- Conditional statements can be applied using the `WHERE` keyword

```SQL
SELECT * FROM table_name WHERE column_name = value -- this gives us all the rows which  adhere to the condition
-- other WHERE usages
SELECT * FROM table_name WHERE column_name > value
SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value -- here, value1 and value are inclusive
SELECT * FROM table_name WHERE column_name = value1 OR column_name = value

-- better way using the IN keyword
SELECT * FROM table_name WHERE column_name IN (value1, value2, value3)
```

## SQL JOINs

SQL JOINs are used to combine rows from two or more tables based on a related column between them. They are essential for querying data across multiple tables in a relational database.

### Types of JOINs

1. **INNER JOIN**
   - Returns only the matching rows from both tables.
   - Syntax:

     ```sql
     SELECT * FROM table1
     INNER JOIN table2 ON table1.column = table2.column;
     ```

2. **LEFT (OUTER) JOIN**
   - Returns all rows from the left table and matching rows from the right table.
   - If no match, NULL values are returned for right table columns.
   - Syntax:

     ```sql
     SELECT * FROM table1
     LEFT JOIN table2 ON table1.column = table2.column;
     ```

3. **RIGHT (OUTER) JOIN**
   - Returns all rows from the right table and matching rows from the left table.
   - If no match, NULL values are returned for left table columns.
   - Syntax:

     ```sql
     SELECT * FROM table1
     RIGHT JOIN table2 ON table1.column = table2.column;
     ```

4. **FULL (OUTER) JOIN**
   - Returns all rows when there's a match in either left or right table.
   - If no match, NULL values are returned for the table without a match.
   - Syntax:

     ```sql
     SELECT * FROM table1
     FULL OUTER JOIN table2 ON table1.column = table2.column;
     ```

5. **CROSS JOIN**
   - Returns the Cartesian product of both tables (all possible combinations).
   - Syntax:

     ```sql
     SELECT * FROM table1
     CROSS JOIN table2;
     ```
