# Relational Data and JOINS

## What is relational data?
	A relation is a table with columns and rows in which data is held. In SQL, sequences and views are also be considered relations.

* **warning:** Relationships and relations are not to be confused. A relation is a data table. A relationship is a connection between data in one table(relation) and data in another table usually based on what those tables represent i.e. data in a customers table may have a relationship with data in an orders table.

From Launch School's [LS180 Database Foundations](https://launchschool.com/courses/019cfcf3/home) course:
> For a developer, relational data can be translated into a more functional definition: working with more than one table at a time. There are many reasons to break data up into multiple tables, and considerations about how tables and their keys and constraints interact affects how rows are retrieved, inserted, updated, and deleted.

## Database Diagrams: Levels of Schema

* Working with database diagrams allows developers to conceptualize a database which aids in implementation.
* When working at the **conceptual level** with diagrams such as entitiy relationship diagrams(ERDs) we are concerned with outlining the different entities and their relationships. We are **not** concerned with the implementation details for any particular database. The conceptual level is highly abstract.
	* Ex: ERD conceptualizing a phone application's data 
    
	![ERD Example.png](/Users/cristianreyes/Creative Cloud Files/ERD Example.png)
    
    * In an ERD entities are represented by squares and their relationships can be represented by lines showing one to one, one to many or many to many relationships.

* When working at the **physical level** we are concerned with the actual implementation of entities and relationships within a particular database. The physical level is very low level and technical.
	*  A physical diagram should contain implementation details such as datatypes, and constraints such as not null, unique, primary key, foreign key etc. which can be represented by simple symbols. Relationships can also be shown by lines connecting for example a primary to a foreign key in another relation.

## Modality 
	Allows us to better describe the relationship between two entities by describing whether or not an instance of each entity is required or optional in a database. The lower bound of how many instances there can be in a relationship.

* Example: The modality going from contact to call is **optional**(0) as contacts may or may not have calls to them. The modality going from call to a contact is **required**(1) as each call must have a contact assigned to it.
* Modality is mostly used at the conceptual level to facilitate the visualization of the relationships between entities.