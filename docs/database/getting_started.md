# Database: Getting Started

 - [Introduction](#introduction)
    - [Configuration](#configuration)
    - [Using Multiple Database Connections](#using-multiple-database-connections)
 - [Using the Database Component](#using-the-database-component)
    - [Running Raw SQL Queries](#running-raw-sql-queries)
    
    
## Introduction 

Framy tries to make database interactions easy. To accomplish this I created a self made database interaction system.

You can interact with your database either using raw sql or soon te implemented the syntax provided by the query builder. In theory every database system should be supported.

### Configuration

The database configuration file is located in `config/database.php`. In this file you may define all your database connections. A example database is provided in this file.

### Using Multiple Database Connections


## Using the Database Component

To access the database functionality to run raw sql queries you can simply use the DB class

```php
DB::select("select * from users");
```

### Running Raw SQL Queries

Once you have configured you database you may run queries using the `DB` class. The DB Manager provides methods for each type of query: select, update, insert and delete.

```php
DB::select("select * from users");
```