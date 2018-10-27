# Database: Query Builder

- [Introduction](#introduction)
- [Retrieving Results](#retrieving-results)
    - [Retrieving All Rows From A Table](#retrieving-all-rows-from-a-table)

## Introduction

Framy's database query builder provides a convenient, fluent interface to creating and running database queries. It can be used to perform most database operations in your application and works on all supported database systems.

The syntax to use is quite similar to sql.

## Retrieving Results

### Retrieving All Rows From A Table

To receiving rows from a table you may use the `select()` method that return the `Query\Builder` class with which you then build your query.

```php
DB()->select()->from('table_name')->get();
```

The `get()` method returns your result as a array of `Model` objects or a single `Model` if only one result is returned.

You may access each column's value by accessing the column as a property of the object: 

```php
foreach($users as $user) {
    echo $user->name;
}
```