# Model

- [Introduction](#introduction)
- [Defining Models](#defining-models)
    - [Model Conventions](#model-conventions)


## Introduction

Each database table has a corresponding "Model" which is used to interact with that table. Models allow you to query for data in your tables, as well as insert new records into the table.

Before getting started, be sure to configure a database connection in `config/database.php`.

## Defining Models

All the models live in the `app/custom/Models` directory. All the models must extend the `app\framework\Component\Database\Model\Model` class.

The easiest way to create a Model is by using the Framy Command:

```
php Framy make:model User
```

### Model Conventions

Now let's look at the `User` Model, which we will use to get retrieve and store data in the `users` table.

```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class User extends Model
{
    //
}
```

### Table Names

Note that we did not specify the table name. By convention, the "snake case", plural name of the class will be used as the table name unless another name is explicitly specified. But this pluralization is currently very basic its just a snake case formatting and an appending "s". 

So in this case Framy assumes that the User Model stores records in the `users` table. You may specify a custom table by defining a table property on your model:

```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class User extends Model
{
    /**
     * The table associated with the model.
     *
     * @var string
     */
    protected $table = 'some_users';
}
```

### Default Attribute Values
If you would like to define the default values for some of your model's attributes, you may define an `$attributes` property on your model:

```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class User extends Model
{
    /**
     * The model's default values for attributes.
     *
     * @var array
     */
    protected $attributes = [
        'isLoggedIn' => false,
    ];
}
```

## Retrieving Models
Once you have created a model and its associated database table, you are ready to start retrieving data from your database. Think of each model as a powerful **query builder**  allowing you to query the database table associated with the model. For example:

```php
<?php

$users = User::all();

foreach ($users as $user) {
    echo $user->name;
}
```

### Adding Additional Constraints

The Model `all` method will return all of the results in the model's table. Since each Model serves as a `query builder`, you may also add constraints to queries, and then use the  `get` method to retrieve the results:

```php
<?php
$users = User::where('created_at', '>', '2018-00-00')
    ->orderBy('name', 'DESC')
    ->take(10)
    ->get();
```

**NOTE**: Since all Models are `query builders`, you should review all of the methods available on the [query builder](query_builder.md). You may use any of these methods in your queries.

## Retrieving Single Models / Aggregates

In addition to retrieving all of the records for a given table, you may also retrieve single records using `find` or `first`. Instead of returning a collection of models, these methods return a single model instance:

```php
// Retrieve a model by its primary key...
$user = User::find(1);

// Retrieve the first model matching the query constraints...
$user = User::where('active', 1)->first();
```

You may also call the `find` method with an array of primary keys, which will return a `ArrayObject` of the matching records:

```php
$users = User::find([1, 2, 3]);
```

### Retrieving Aggregates
You may also use the `count`, `sum`, `max`, and other aggregate methods provided by the `query builder`. These methods return the appropriate scalar value instead of a full model instance:

```php
$count = User::where('active', 1)->count();

$max = User::where('active', 1)->max('price');
```
