# Database: Query Builder

- [Introduction](#introduction)

## Introduction

Framy's database query builder provides a convenient, fluent interface to creating and running database queries. It can be used to perform most database operations in your application and works on all supported database systems.

The query builder uses PDO parameter binding to protect your application against SQL injection attacks. There is no need to clean strings being passed as bindings.

## Retrieving Results

### Retrieving All Rows From A Table

You may use the table method on the DB class to begin a query. The table method returns a query builder instance for the given table, allowing you to chain more constraints onto the query and then finally get the results using the get method: 

```php
$users = DB::table('users')->get();
```

The `get()` method returns a array containing the results where each result is an instance of `Model` class. You may access each column's value by accessing the column as a property of the object:

```php
foreach ($users as $user) {
    echo $user->name;
}
```

### Retrieving A Single Row / Column From A Table

If you just need to retrieve a single row from the database table, you may use the first method. This method will return a single `Model` object:

```php
$user = DB::table('users')->where('name', 'John')->first();
```

If you don't even need an entire row, you may extract a single value from a record using the  value method. This method will return the value of the column directly:

```php
$user = DB::table('users')->where('name', 'John')->value("name");
```

## Aggregates
The query builder also provides a variety of aggregate methods such as `count`, `max`, `min`,  `avg`, and `sum`. You may call any of these methods after constructing your query:

```php 
$users = DB::table('users')->count();

$price = DB::table('orders')->max('price');
```

### Determining If Records Exist

Instead of using the count method to determine if any records exist that match your query's constraints, you may use the exists and doesntExist methods:

```php
return DB::table('orders')->where('finalized', 1)->exists();

return DB::table('orders')->where('finalized', 1)->doesntExist();
```