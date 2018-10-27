# Database: Getting Started

 - [Introduction](#introduction)
    - [Configuration](#configuration)
    - [Using Multiple Database Connections](#using-multiple-database-connections)
 - [Using the Database Component](#using-the-database-component)
    - [Running Raw SQL Queries](#running-raw-sql-queries)
    
    
## Introduction 

Framy tries to make database interactions easy. To accomplish this I created a self made database interaction system.

You can interact with your database either using raw sql or the syntax provided by the query builder. In theory every database system should be supported. All classes of the component return there results as models. 

### Configuration

The database configuration file is located in `config/database.php`. In this file you may define all your database connections. A example data base in provided in this file.

### Using Multiple Database Connections

When using multiple connections, you may access each connection via the `useConnection()` method of the `Database\Manager` class. The name passed to the connection method should correspond to one of the connections listed in your config/database.php configuration file.

## Using the Database Component

To work with the database we need the helper function `DB()`:

```php
DB();
``` 
Leave arguments blank for default connection.

### Running Raw SQL Queries

Once you have configured you database you may run queries using the helper function `DB()`. The DB Manager provides methods for each type of query: select, update, insert and delete.

```php
DB()->getConnection()->select("select * from users");
```