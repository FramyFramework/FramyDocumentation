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

#### whereBetween / orWhereBetween  

The whereBetween method verifies that a column's value is between two values:

```php
$users = DB::table('users')
    ->whereBetween('votes', [1, 100])->get();
```

#### whereNotBetween / orWhereNotBetween

The `whereNotBetween` method verifies that a column's value lies outside of two values:

```php
$users = DB::table('users')
    ->whereNotBetween('votes', [1, 100])->get();
```

#### whereIn / whereNotIn / orWhereIn / orWhereNotIn
     
The `whereIn` method verifies that a given column's value is contained within the given array:

```php
$users = DB::table('users')
    ->whereIn('votes', [1, 100])->get();
```

The `whereNotIn` method verifies that the given column's value is not contained in the given array:

```php
$users = DB::table('users')
    ->whereNotIn('votes', [1, 100])->get();
```

#### whereNull / whereNotNull / orWhereNull / orWhereNotNull
     
The `whereNull` method verifies that the value of the given column is `NULL`:

```php
$users = DB::table('users')
    ->whereNull('updated_at')->get();
```

The `whereNotNull` method verifies that the column's value is **not** `NULL`:

```php
$users = DB::table('users')
    ->whereNotNull('updated_at')->get();
```

#### whereDate / whereMonth / whereDay / whereYear / whereTime
     
The `whereDate` method may be used to compare a column's value against a date:

```php
$users = DB::table("users")
    ->whereDate("created_at", "=", "2019-04-06")->get();
```

The `whereMonth` method may be used to compare a column's value against a specific month of a year:

```php
$users = DB::table("users")
    ->whereMonth("created_at", "=", 4)->get();
```

The `whereDay` method may be used to compare a column's value against a specific day of a month:

```php
$users = DB::table("users")
    ->whereDay("created_at", "=", 6)->get();
```

The `whereYear` method may be used to compare a column's value against a specific year:

```php
$users = DB::table("users")
    ->whereYear("created_at", "=", 2019)->get();
```

## Ordering, Grouping, Limit, & Offset

#### orderBy
The `orderBy` method allows you to sort the result of the query by a given column. The first argument to the `orderBy` method should be the column you wish to sort by, while the second argument controls the direction of the sort and may be either `asc` or `desc`:

```php
$users = DB::table('users')
    ->orderBy('name', 'desc')
    ->get();
```

#### latest / oldest
The `latest` and `oldest` methods allow you to easily order results by date. By default, result will be ordered by the `created_at` column. Or, you may pass the column name that you wish to sort by:

```php
$user = DB::table('users')
    ->latest()
    ->first();
```

#### inRandomOrder
The `inRandomOrder` method may be used to sort the query results randomly. For example, you may use this method to fetch a random user:

```php
$randomUser = DB::table('users')
    ->inRandomOrder()
    ->first();
```

#### skip / take
To limit the number of results returned from the query, or to skip a given number of results in the query, you may use the `skip` and `take` methods:

```php
users = DB::table('users')->skip(10)->take(5)->get();
```

Alternatively, you may use the limit and offset methods:

```php
$users = DB::table('users')
    ->offset(10)
    ->limit(5)
    ->get();
```

## Inserts
The query builder also provides an insert method for inserting records into the database table. The insert method accepts an array of column names and values:

```php
DB::table('users')->insert(
    ['email' => 'john@example.com', 'votes' => 0]
);
```

You may even insert several records into the table with a single call to insert by passing an array of arrays. Each array represents a row to be inserted into the table:

```php
DB::table('users')->insert([
    ['email' => 'taylor@example.com', 'votes' => 0],
    ['email' => 'dayle@example.com', 'votes' => 0]
]);
```

## Updates
In addition to inserting records into the database, the query builder can also update existing records using the `update` method. The `update` method, like the `insert` method, accepts an array of column and value pairs containing the columns to be updated. You may constrain the  `update` query using `where` clauses:

```php
DB::table('users')
    ->where('id', '=', 1)
    ->update(['votes' => 1]);
```

### Increment & Decrement
The query builder also provides convenient methods for incrementing or decrementing the value of a given column. This is a shortcut, providing a more expressive and terse interface compared to manually writing the `update` statement.

Both of these methods accept at least one argument: the column to modify. A second argument may optionally be passed to control the amount by which the column should be incremented or decremented:

```php
DB::table('users')->increment('votes');

DB::table('users')->increment('votes', 5);

DB::table('users')->decrement('votes');

DB::table('users')->decrement('votes', 5);
```

## Deletes
The query builder may also be used to delete records from the table via the `delete` method. You may constrain `delete` statements by adding `where` clauses before calling the `delete` method:

```php
DB::table('users')->delete();

DB::table('users')->where('votes', '>', 100)->delete();
```

If you wish to truncate the entire table, which will remove all rows and reset the auto-incrementing ID to zero, you may use the `truncate` method:

```php
DB::table('users')->truncate();
```