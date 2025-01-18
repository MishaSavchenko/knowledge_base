## MySQL

Refs: [guru99](https://www.guru99.com/mysql-tutorial.html)

* Databases  
  * Systemic collection of data  
* DBMS (Database Management System)  
  * Access, manipulate, report and represent data  
  * DBMS evolved in the following way   
    * Navigational \-\> Relational \-\> SQL \-\> Object Oriented  
  * Types of DBMS  
    * Hierarchical  
      * Parent child relationship (\*) of storing data  
      * Outdate   
      * E.x. WIndows XP registry   
    * Network   
      * Supports many-to-many relations (\*)  
      * Complex database structures   
      * Ex. RDM Server   
    * Relational   
      * Relationships in form of tbles   
      * Does not support many to many   
      * Supports predefined daya types  
      * Most popular type   
      * Ex. MySQL, Oracle Mucrosoft SQL Server   
    * Object Oriented Relational   
      * Supports storage of new data types   
      * Stores objects with attributes and methods that define what to do with the data   
      * Ex. PostgreSQL  
* SQL (Structured Query Language)   
  * Standard language for dealing with Relational Databases   
  * insert , search, update, delete functionality  
  * Also optimizes and maintas databases  
  * Ex of SQL syntax: SELECT \* FROM Members WHERE Age \> 30   
  * Advantages   
    * Mature data storage and managemnet model   
    * Support notion of views   
      * Allowing only the authorized to view the data   
    * Better security models compared to NoSQL  
* NoSQL   
  * Non adherence to relational database concepts   
  * Huge database tend to be slow and the first solutions is scaling up (upgrading hardware) or scaling out ( distribute the database load between multiple hosts )  
  * NoSQL databases scale out and designed with web applications in mind  
  * Do not follow stict schemas like relational models   
  * ACID features arent guaranteed (\*)  
    * Atomicity   
    * Consistency   
    * Isolation   
    * Durability  
  * More suited for large volumes of data   
  *   
* MySQL Advantages   
  * Supports multiple storage engines  
  * High performance compared to other relation database systems  
  * Cost effective   
    * Comunity edition is free  
  * Cross platform   
* Server Access tool  
  * Allows for interaction with MySQL   
  * MySQLWorkbench   
    * Visual database designing and modeling access tool   
    * Allows for creation of new physical data models and modification of existing MySQL databases with reverse/forward engineering and change management functions   
    * Modeling and Design Tool  
      * Models as the core of valid and high performance databases  
      * Supports creation of multiple models in the same environment   
      * Supports all objects   
        * Tables  
        * views   
        * Stored procedures  
        * Triggers  
      * Built in model validating utility   
        * Reports any isssues that make up a database  
      * Supports different modeling notation and can be extended using LUA   
    * SQL Development Tool   
      * MySQL has a built in visual editor   
      * Allows to build edit and run queries against server databases   
      * Allows to view and export data  
      * Supports syntax color highlighters  
      * Multiple queries can be run   
    * Administration Tool  
      * User administration  
        * Manage users  
          * add/remove users  
          * grant/drop privileges  
          * View user profiles  
      * Server Configuration  
        * Advanced configuration of the server and fine tunning for optimal performance   
      * Database backup and restorations  
        * Exporting/importing dump files  
          *  Which contain scripts for creating databases, tablees, views, stored procedures and insertion of data  
      * Server Logs  
        * Views server logs   
          * Error logs, binary logs, InnodDB logs  
        * Diagnosis of server  
* Database Design  
  * Collection of processes that facilitate the designing, development, implementation and maintenance of enterprise data management systems   
  * Main objectives is to produce logical and physical design models of the proposed database system   
    * Logical model   
      * Data requirement   
      * Data independents of physical considerations   
      * Doesnt concern itself with how or where the data is stored   
    * Physical model   
      * Translates the ogical design into physical media using hardware resources and DBMS systems  
  * Importance of database design  
    * Yields in high performance   
    * Ease of maintainance   
    * Data consistency   
    * Cost effectinveness (disk storage space)  
  * Database develepment life cycle   
    * Requirements analysis \-\> Database designing \-\> Implementation  
    * Requirements analysis   
      * Planning   
        * Plannign the entire Database Deveopment Lfie Ccle   
      * System Definition   
        * Defines the scope and boundaries of the proposed database system   
    * Database designing   
      * Logical model   
      * Physical model   
    * Implementaton   
      * Data conversion and loading   
        * Importing and converting data from the old system into the new database  
      * Testing   
        * Identification of error in the newly implemented system   
        * Check the database againstrequirement specifications

## Database Techniques

* Normalization   
  * Organization of tables that reduces redundancy and dependency of data   
  * Larger tables are divided into smaller table and linked using relationships   
  * Normalization achieve its best in 3rd Normal From   
  *  Forms   
    * First Normal Form (1NF)  
      * Each table cel should contain a single value   
      * Each record needs to be unique   
    * Second Normal Form (2NF)  
      * Be in 1NF  
      * Single Column Primary key  
    * Third Normal Form (3NF)  
      * Be in 2NF  
      * Has no transitive functional dependencies   
    * Boyce-Codd Normal Form (BCNF/3.5NF)  
      * Anomalies may occur when there is more than one Candidate Key (when in 3NF)  
    * Fourth Normal Form (4NF)  
      * No database table instance contains two or more indepeendent and multivalued data describing the relevant entitiy   
    * Fifth Normal Form (5NF)  
      * If 4NF cannot be decomposed into smaller tables without loss of data  
    * Sixth Normal Form (6NF)  
      * Experimental and non standardized  
  * KEY   
    * Value that is used to identify a record in a table uniquely   
    * Single or combination of multiple columns   
    * Non-key columns   
      * Columns in a table that are NOT used to identify a record uniquely   
    * Primary non-key   
      * Single column value   
      * Cannot be NULL   
      * Must be unique  
      * Should be rarely changed   
      * Must be given a value when a new record is inserted   
    * Composite Key   
      * Primary key composed of multiple columns   
      * E.x multiple people with the smae name but live on diffeernet address   
    * Foreign Key   
      * Primary key of another table   
      * Can have a different name from its primary key   
      * Ensures row in one table have a corresponding rows in another   
      * Do not have to be unique   
      * Can be null   
      * Helps to prevent cross table insertion errors  
      *   
    * Transitive functional dependencies   
      * Changin a non-key column may cause any of the other non-key columns to change   
  *   
* ER Modeling  
  * Graphical approach  
  * Entity/Relationship to represent real world objects  
  * Entity   
    * Has a set of properties   
    * Properties can have values   
  * Enhanced Entity Relationship (EER) Model   
    * More complex ER modeling   
    * Uses UML notation (Unified Modeling Language)   
    * Step to develop EER diagram   
      * Identify the entities and determine the relationships   
      * Each entity attribute and relationshiop should have appropriate names that can be easily understood by the non0technical people   
      * Relationshipt should connected to entities not to each other   
      * Attribute in a given entity should have a unique name   
* Creating Database   
  * 

PostgreSQL

* 

Databases 

* Data Integrity  
  * Can handle massive amounts of data  
* Quickly combine different datasets  
* Automate steps for re-use  
* Support data for websites and applications

PgAdmin