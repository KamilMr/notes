# SQL
SQL is a standard language for storing, manipulating and retrieving data in databases.

## MySQL Data Types
[Data Types](https://www.w3schools.com/sql/sql_datatypes.asp)

`CREATE DATABASE databasename;`
The CREATE DATABASE statement is used to create a new SQL database.

`FOREIGN KEY`
The FOREIGN KEY constraint is used to prevent actions that would destroy links between tables. A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.

The FOREIGN KEY constraint prevents invalid data from being inserted into the foreign key column, because it has to be one of the values contained in the parent table.

`PRIMARY KEY`
The PRIMARY KEY constraint uniquely identifies each record in a table. Primary keys must contain UNIQUE values, and cannot contain NULL values.
A table can have only ONE primary key; and in the table, this primary key can consist of single or multiple columns (fields).

`CONSTRAINTS`
Constraints can be specified when the table is created with the CREATE TABLE statement, or after the table is created with the ALTER TABLE statement.

SQL constraints are used to specify rules for the data in a table. Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

`ALTER`
The ALTER TABLE statement is used to add, delete, or modify columns in an existing table.

The ALTER TABLE statement is also used to add and drop various constraints on an existing table.

`ENUM`
An ENUM is a string object with a value chosen from a list of permitted values that are enumerated explicitly in the column specification at table creation time.

[ENUM](https://dev.mysql.com/doc/refman/8.0/en/enum.html)

example: `ENUM('x-small', 'small', 'medium', 'large', 'x-large')`
 If an ENUM column is declared NOT NULL, its default value is the first element of the list of permitted values.
