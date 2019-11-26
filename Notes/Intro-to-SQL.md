# Introduction to SQL

## The Importance of Data
Tools that allow us to access data are invaluable today in all areas of life, whether it be in a field such as baseball scouting or genetic science. We make decisions from the study and interpretation of data but in order to interpret data effectively we must structure it.

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
* SQL is declarative - you specify what needs to be done, and the implementation is handled under the hood by the rdms.

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

#### PostgreSQL Column Data Types
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
	* CHECK - constraint that provides a condition that data entered must match in order to be valid.
	
### Altering Tables

* ```ALTER TABLE``` is used to change the schema of a table, not the data
* Altering tables follows the syntax: ```ALTER TABLE table_name HOW TO ALTER TABLE additional_arguments ```
##### Renaming a table
	```SQL
   ALTER TABLE table_name 
   RENAME TO new_name;```
##### Deleteing a table
warning: ***irreversible***
```SQL
DROP TABLE table_name
```
##### Adding a column
```SQL
ALTER TABLE table_name
ADD COLUMN column_name data_type constraints;
```
##### Removing a column
warning: ***irreversible***
```SQL
ALTER TABLE table_name
DROP COLUMN column_name;
```
##### Renaming a column
	```SQL
    ALTER TABLE table_name
    RENAME COLUMN column_name TO new_name;
    ```
##### Changing column data type
	```SQL
    ALTER TABLE table_name
    ALTER COLUMN column_name TYPE data_type;
    ```
##### Adding a constraint
* Most of the time, rather than modifying constraints, we will be removing and adding constraints. 
* Some constraints are column specific. They can be added by:
```SQL
ALTER TABLE table_name
ALTER COLUMN column_name SET constraint_name constraint_clause;
```
* Some constraints are table specific and can be added by:
```SQL
ALTER TABLE table_name
ADD CONSTRAINT constraint_name constraint_clause;
```
##### Removing a constraint
* Column constraints can be removed by:
```SQL
ALTER TABLE table_name
ALTER COLUMN column_name DROP CONSTRAINT constraint_name;
```
* Table constraints can be removed by:
```SQL
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```
##### Removing a default
```SQL
ALTER TABLE table_name
ALTER COLUMN column_name DROP DEFAULT;
```

## Data and DML
	data manipulation language (DML) consists of the SQL statements that allow us to access and manipulate data in the database.

* Four types of DML statements:
	1. Insert (adds data to the database)
	2. Select (a.k.a. queries, provide access to existing data)
	3. Update (update existing data)
	4. Delete (deletes existing data from database)

### Insertion Statement Syntax
* General insertion statement syntax:
```SQL
INSERT INTO table_name(column1_name, column2_name ...)
	VALUES(data_for_column1, data_for_column2 ...);
```

* Insertion statements require:
	1. table name
	2. name of columns we are inserting data into
		* If no columns are specified, value order must match the schema of the table
		* If some columns are specified, unspecified columns will recieve a null or default value.
	3. The values we wish to store in the columns listed directly after the table name.
		* should be ordered according to #2 listed columns or if none  were listed,  according to the table schema.

* Insert statements add rows to our database. Each row is an individual entity analogous to a record.
* Multiple rows can be added in one insert statement by comma separating values i.e.:
```SQL
INSERT INTO table_name(column1_name, ...)
	VALUES(row_1_column_1, row1_column_... ),
    	  (row_2_column_1, row2_column_...),
           ...;
```

### Select Statements
* General select statement syntax:
```SQL
SELECT [*, (column_name, column2_name, ...)]
FROM table_name WHERE (condition);
```
* Select statements are formed by identifiers( words that identify columns/tables) and keywords (SELECT, FROM , WHERE, etc.)
	*  If  an identifier is the same as a keyword, we must surround it in double quotes in order to prevent an error.

#### Order By
* ```ORDER BY``` example syntax:
```SQL
SELECT * FROM table_name
WHERE some_condition
ORDER BY column_name DESC
```
* Like a ```WHERE``` clause, an ```ORDER BY``` clause is used to filter results.
	* rather than a condition, ```ORDER BY``` clauses take a column(or multiple comma separated columns) to filter query results by a sorting order.
* ```ORDER BY``` sorts query results by ascending order as default, but this can be changed by specifying ```DESC``` in the clause.
* Specifying multiple columns to sort by creates sorting sublevels.

#### Operators
	Typically used within a WHERE clause, operators make our queries more powerful.
* Operators can be placed under 3 groups:
	1. Comparison
	2. Logical
	3. String Matching

##### Comparison Operators
	Operators used to compare two values
| Operator | Description |
|--------|--------|
|>=      |greater than or equal|
|<=|less than or equal|
|<> or !=| not equal|
|=| is equal|
|>| greater than|
|<| less than|

* Includes comparison predicates i.e. ```IS NULL```, ```NOT NULL```, ```BETWEEN```, ```NOT BETWEEN```

##### Logical Operators
	Used to provide more flexibility to our conditions

* Three logical operators:
	1. ```AND```
	2. ```OR```
	3.  ```NOT```

##### String Matching Operators
	Used only with data that is a string, looks to match a column's value to a string matching expression

* ```LIKE``` operator - used to match against a string.
	* Example Syntax:  
	```SQL
    SELECT * FROM users WHERE last_name LIKE "%Smith"
    ```
    	* ```%``` wildcard matches any number of characters
    	* ```_``` wildcard matches a sing character.

* ```SIMILAR TO``` operator - used to match against a regexp

#### Limit and Offset
	These filtering criteria are the basis for pagination - the user experience feature of dividing data between different pages.

* **Limit:** Determines the amount of rows/records that a query returns.
* **Offset:** Determines the start of query results displayed based on the distance from the first query result.

#### Distinct
	Keyword used to filter query results for unique values only.

* Ex:
```SQL
	SELECT DISTINCT full_name FROM users;
```
returns only unique full names from the users table.

### Functions
	Commands that may be called on data to transform data before it is returned or to return information on data.

* Can be grouped into these types of functions:
	* String
	* Date/Time
	* Aggregate 

#### String Functions
	Functions which may operate on string data types

* Ex:
| Function | Example | Notes|
|--------|--------|--------|
| length | SELECT length(full_name) FROM USERS; |This returns the length of every user's name. You could also use length in a WHERE clause to filter data based on name length.|
|trim|SELECT trim(leading ' ' from full_name) FROM users;|If any of the data in our full_name column had a space in front of the name, using the trim function like this would remove that leading space.

#### Date/Time Functions
	Functions which operate mostly on timestamp/date data.

* Ex:
| Function | Example | Notes |
|--------|--------|--------|
| date_part | SELECT full_name, date_part('year', last_login) FROM users; | date_part allow us to view a table that only contains a part of a user's timestamp that we specify. The above query allows us to see each user's name along with the year of the last_login date. Sometimes having date/time data down to the second isn't needed|
| age | SELECT full_name, age(last_login) FROM users; | The age function, when passed a single timestamp as an argument, calculates the time elapsed between that timestamp and the current time. The above query allows us to see how long it has been since each user last logged in. |

#### Aggregate Functions
	Functions which perform aggregation- returning a single result from a set of input data

* Ex:
| Function | Example | Notes |
|--------|--------|-|
|count| SELECT count(id) FROM users; | Returns the number of values in the column passed in as an argument. This type of function can be very useful depending on the context. We could find the number of users who have enabled account, or even how many users have certain last names if we use the above statement with other clauses. |
| sum | SELECT sum(id) FROM users; | Not to be confused with count. This sums numeric type values for all of the selected rows and returns the total. |
| min | SELECT min(last_login) FROM users; | This returns the lowest value in a column for all of the selected rows. Can be used with various data types such as numeric, date/ time, and string. |
| max | SELECT max(last_login) FROM users; | This returns the highest value in a column for all of the selected rows. Can be used with various data types such as numeric, date/ time, and string. |
| avg | SELECT avg(id) FROM users; | Returns the average (arithmetic mean) of numeric type values for all of the selected rows. |

### Group By
	Allows for the grouping of data by some data in some column or the results of a function.
    
   * Ex: * Groups the data by the values in the enabled column and returns the counts of both groups*
```
sql_book=# SELECT enabled, count(id) FROM users GROUP BY enabled;
 enabled | count
---------+-------
 f       |     1
 t       |     4
(2 rows)
```