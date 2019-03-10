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

## Where Clauses

### Simple Where Clauses

You may use the `where()` method on a query builder instance to add `where` clauses to the query. The most basic call to `where()` requires three arguments. The first argument is the name of the column. The second argument is an operator, which can be any of the database's supported operators. Finally, the third argument is the value to evaluate against the column.

For example, here is a query that verifies the value of the "votes" column is equal to 100:

```php
$users = DB::table('users')->where('votes', '=', 100)->get();
```

You may use a variety of other operators when writing a where clause:

```php
$users = DB::table('users')
    ->where('votes', '>=', 100)
    ->get();

$users = DB::table('users')
    ->where('votes', '<>', 100)
    ->get();

$users = DB::table('users')
    ->where('name', 'like', 'T%')
    ->get();
```

You may also pass an array of conditions to the where function:
    
```php
$users = DB::table('users')->where([
    ['status', '=', '1'],
    ['subscribed', '<>', '1'],
])->get();
```

### Or Statements
You may chain where constraints together as well as add or clauses to the query. The  orWhere method accepts the same arguments as the where method:

```php
$users = DB::table('users')
    ->where('votes', '>', 100)
    ->orWhere('name', 'John')
    ->get();
```

### Additional Where Clauses

#### whereBetween

The whereBetween method verifies that a column's value is between two values:

```php
$users = DB::table('users')
    ->whereBetween('votes', [1, 100])->get();
```
