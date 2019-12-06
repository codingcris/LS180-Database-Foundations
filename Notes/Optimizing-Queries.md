# Optimizing SQL Queries
## Indexes
	A mechanism for speeding up SQL Queries. Similar to an index in a textbook, an index in SQL points to a row's position in a table.

* Ex: A query for all books by a particular author without an index would have to search row by row through the table. With an index, the search would be much shorter in the index table.
![Image credit to Launch School's Database Foundations Course](https://da77jsbdz4r05.cloudfront.net/images/optimizing_queries/books_table_highlighted_index.png) 

### When to use an index?
* Using indexes can optimize a table's reads but cost in terms of write performance.
	* Every time an indexed column is updated or inserted the index table must be updated as well 


From Launch School's [Database Foundations](https://launchschool.com/lessons/e752508c/assignments/17c58bc3) Course:

> * Indexes are best used in cases where sequential reading is inadequate. For example: columns that aid in mapping relationships (such as Foreign Key columns), or columns that are frequently used as part of an ORDER BY clause, are good candidates for indexing.
* They are best used in tables and/ or columns where the data will be read much more frequently than it is created or updated.

* There are different types of indexes available in PSQL (i.e. B-tree, Hash, GiST, and GIN) using different data structures and algorithms. Index type is an important design consideration.

### Creating Indexes
* An index is created implicitly when a public key is declared or a UNIQUE constraint is set. Indexes are the mechanism by which these columns are maintained unique.
* Foreign key constraints do not create an index by default but are good candidates for indexing.
* General form for creating a column index:

``` SQL
CREATE INDEX index_name ON table_name(column_name);
```
* PSQL uses B-tree as the default index type

### Unique and Non Unique Indexes
* Indexes enforcing the unique constraint are unique indexes which do not permit duplicate values in a column. A non unique index permits duplicate values in the column.

### Multicolumn Indexes
* Certain index types support multiple columns. 

```SQL
CREATE INDEX index_name ON table_name(column1, column2, ...);
```

### Partial Indexes
* Indexes can be created for subsets of data in a column that match a particular condition. The index will contain only entries for the rows that match this condition.

### Deleting Indexes

```SQL
DROP INDEX index_name;
```

## Comparing SQL Statements
	While the SQL language is declarative and implementation details are abstracted away by the database engine, we can influence the process of how a query runs by the way that we structure our query. In large datasets, the time savings from one type of query compared to another query that returns the same results may be a worthwhile optimization.

### Assesing a Query With Explain
* ```EXPLAIN``` keyword preceding a query will give us the query plan PSQL will use to execute the query although the query will not be executed. 
	* query plan is returned in the form of a node tree 
	* query plan contains the steps as well as the performance costs (arbitrarily chosen by the planner) of each step.
* USING ``ANALYZE`` keyword following ```EXPLAIN```keyword and preceding a query will execute the query and return the actual time in milliseconds taken for each node in the query plan to execute

## Subqueries
	Subqueries can perform better than join statements in certain situations and allow us to nest queries. They should be considered for forming good queries.

### Subquery Expressions
* ```EXISTS``` checks whether any rows are returned by a nested query
* ```IN``` and ```NOT IN``` check whether the results of a query are in or absent in the results of a nested query.
* ```ANY```/```SOME``` from Launch School's [Database Foundations](https://launchschool.com/lessons/e752508c/assignments/2009d549) course:

>ANY and SOME are synonyms, and can be used interchangeably. These expressions are used along with an operator (e.g. =, <, >, etc). The result of ANY / SOME is 'true' if any true result is obtained when the expression to the left of the operator is evaluated using that operator against the results of the nested query.

* ```ALL```  from Launch School's [Database Foundations

>As with ANY / SOME, ALL is used along with an operator. The result of ALL is true only if all of the results are true when the expression to the left of the operator is evaluated using that operator against the results of the nested query.

