# Getting Started

- [Introduction](#introduction)
    - [General Usage](#general-usage)
    - [Running Raw SQL Query](#running-raw-sql-queries)
        - [Running A Select Query](#running-a-select-query)
        - [Running An Insert Statement](#running-an-insert-statement)
        - [Running An Update Statement](#running-an-update-statement)
        - [Running A Delete Statement](#running-a-delete-statement)

## Introduction

Framy tries to make database interaction very simple across a variety of database beckends using either raw SQL or the query builder that will soon be added.

## General Usage 

After configuring an connection. Simply create a Instance of the DatabaseManager, no arguments neede if default (or only) configured connection should be used.

## Running Raw SQL Queries

Once you configured your database connection, you may run queries using the DB class. The DB class provides methods for each type of query: `select`, `update`, `insert` and `delete`.

### Running A Select Query

To run a basic query, you may use the select method on the DB class.

```php
$user = DB::select("select * from users where id=:id", ['id'=>12]);
```

### Running An Insert Statement

To execute an insert statement, you may use the insert method on the DB class.

```php
DB::insert("insert into user (username, password) VALUES [...] ");
```

### Running An Update Statement

The update method should be used to update existing records in the database. The number of rows affected by the statement will be returned:

```php
$affected = DB::update('update users set votes = 100 where name = ?', ['John']);
```

### Running A Delete Statement

The delete method should be used to delete records from the database. Like update, the number of rows affected will be returned:

```php
$deleted = DB::delete('delete from users');
```
