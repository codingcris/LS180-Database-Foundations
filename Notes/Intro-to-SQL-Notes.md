# Introduction to SQL

## The Importance of Data
Tools that allow us to access data are invaluable today in all areas of life, whether it be in a field such as baseball scouting or genetic science. Data helps us to make decisions from the study and interpretation of data, but in order to interpret data effectively, we must structure it.

## Structured Data
As datasets grow in size and complexity, it is important to structure data in a way that allows users to access and analyze the data efficiently.

- Spreadsheets are a simple way of structuring data. They are analogous to a database.
|                 |              |
|-----------------|--------------|
|spreadsheet      |database      |
|worksheet        |table         |
|worksheet column | table column |
|worksheet row    | table row    |

* In a corporate setting, many editors may have acccess to a spreadsheet, and this can be the cause of problems such as formatting of data, ability to search through the data, typos, duplicate data etc. For this setting, a *relational database management system* is preferred.

## Relational Database Management Systems
- **relational database:** A database organized according to the relational model of data. The relational model of data defines a set of relations (a set of individual but related data entries analogous to tables) and the connections between them to specify how data stored in them can interact.
- **relational database management system:** software that allows a user to interact with a database through commands falling under certain conventions or standards. SQL is the underlying language to all rdms'.
EX: SQLite, MSSQL, PostgreSQL, MySQL.

## SQL
Structured Query Language - The programming language used to communicate with a relational database.
* SQL allows you to use simple English sentences to insert, update, delete, or select large amounts of data.
* SQL is declerative - you specify what needs to be done, and the implementation is handled under the hood by the rdms.

## The psql Console
	psql is a client application that allows us to interact with a PostgreSQL database from terminal.
* ```psql postgres``` command opens up the psql console and connects it to the postgres database (default database created when installing PostgreSQL)
* **2 Types of commands that can be isssued from the psql console:**
	1. psql console meta-commands
	2. SQL queries using standard SQL syntax.

### Meta Commands
	Meta commands are written with a backslash followed by the command and optional arguments. They can be used to connect to a different database, list tables, setting environment variables, etc.

* ```\conninfo``` gives all relevant connection information for the current connection to database.
* ```\q``` quits psql console
* ```\l``` or ```\list``` lists all databases
* ```\c``` or ```\connect``` will close the connection to the current database and establish a new connection to the specified database.
* ```\dt``` provides a list of all tables/relations in the database.
* ```\d``` followed by the name of a table allows us to see detailed information on the table's columns.

### SQL Statements
	Commands issued to the database using SQL syntax. Must always end with a semicolon and can span multiple lines.
* ```SELECT``` statements are used to retrieve data from a database.
* ```CREATE TABLE``` statement used to create a table in the database
* ```DROP TABLE``` statement used to delete a table in the database.
* etc.

## SQL Sub-languages
SQL can be thought of as comprised of 3 separate sub-languages all concerned with a specific aspect of manipulating or interacting with a database.
1. **DDL: Data Definition Language:** used to define the structure of a database and the tables and columns within it.
2. **DML: Data Manipulation Language:** used to retrieve or modify data stored in database.
3. **DCL: Data Control Language:** used to determine what various users are allowed to do when interacting with a database.

## Data v.s. Schema
The relationship between data and schema is what gives a database power.
    
* Schema is concerned with the structure of data within a database (column and row names, table names, data types within each column and row, etc.) 
* Data is concerned with the actual values that go into each row and column of a database. 
* SQL's DDL sub-language is used to manipulate schema. 
* SQL's DML sub-language is used to manipulate data.

** Without schema, data would have no structure. Without data, we would simply have column and row names with no values. Data and schema together allow us to interact with databases in powerful ways. **

## SQL Forming and Deleting Databases

### Creating Databases
* We can create a database using the ```createdb``` command from terminal, or using the SQL command ```CREATE DATABASE``` from the psql console with mandatory argument for the database name.
* Database names should be descriptive and snake_case by convention.

### Deleting Databases
* We can delete a database using the ```dropdb``` command from terminal which is a wrapper for the SQL command ```DROP DATABASE``` followed by the mandatory database_name argument.
* These functions are permanent. Use with caution.

### Creating Tables
* We can create a table within a database using the SQL command ```CREATE TABLE``` followed by the table_name(). *note parentheses*
* Inside of a new table name's parentheses, we must place column definitions.
	* Column definitions specify a column name (required), the data type (required), and *constraints* (optional).
	* Column definitions should be comma separated.

* Basic format for CREATE TABLE is:
```SQL
CREATE TABLE table_name (
  column_1_name  column_1_data_type  [constraints, ...],
  column_2_name  column_2_data_type  [constraints, ...],
  .
  .
  .
  constraints
);```

*  Constraints may be placed at the column or table level.

#### Column Data Types
* Data types protect our tables from incorrect data being entered 

|Column Data Type|Purpose|
|----------------|-------|
|serial          | Serial data types are self incrementing unique integers which must not be null.|
|char(N)         | Strings up to N characters in length. If the string is less than N characters long, spaces are used to fill the remanining characters.|
|varchar(N)      |Strings up to N characters in length. Data that contains less than N characters will not be filled in with spaces.|
|boolean         | "true" or "false"|
|integer or INT  | Whole numbers|
|decimal(precision, scale)|Decimal type takes two arguments: **1. Precision:** *total number of digits on left and right side of decimal* **2. Scale:** *number of digits to the right of the decimal.*|
|timestamp       | Represents the data and time in simple YYYY-M-D HH:MM:SS format|
|date            | Represents the date in YYYY-M-D format without time.|

#### Keys and Constraints
* Constraints are optional.
* Constraints preserve the integrity of the database by defining the types of values that can be held in a column.
* Ex: 
	* DEFAULT- takes a value that will be placed in the column should the value entered in the column be empty.
	* NOT NULL- specifies that the column must contain some data rather than be empty.
	* UNIQUE- prevents duplicate values from being entered into the column.

### Altering Tables

* ```ALTER TABLE``` is used to change the schema of a table, not the data
* Altering tables follows the syntax: ```ALTER TABLE table_name HOW TO ALTER TABLE additional_arguments ```
##### Renaming a table
	```SQL
   ALTER TABLE table_name 
   RENAME TO new_name;```


