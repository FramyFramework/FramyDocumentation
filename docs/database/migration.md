# Database: Migrations

 - [Introduction](#introduction)
 - [Generating Migrations](#generating-migrations)
 - [Migration Structure](#migration-structure)
 - [Running Migrations](#running-migrations)
 - [Tables](#tables)
    - [Creating Tables](#creating-tables)
 - [Columns](#columns)
    - [Creating Columns](#creating-columns)
    - [Available Column Types](#available-column-types)

## Introduction

Migrations are like version control for your database, allowing your team to easily modify and share the application's database schema.

## Generating Migrations


To create a migration, use the `make:migration` Framy Command.

```
php Framy make:migration users_table connection
```

The new migration will be placed in your `/app/custom/database/migration` folder.

## Migration Structure

A migration class contains two methods: `up` and `down`. The `up` method is used to add new tables, columns, or indexes to your database, while the `down` method should reverse the operations performed by the `up` method.

## Running Migrations

To run all of your outstanding migrations, execute the migrate Artisan command:

```
php Framy migrate
```

## Tables

### Creating Tables
To create a new database table, use the `create` method on the Schema class.
The `create` method accepts three arguments.

## Columns

### Creating Columns

The `table` method on the Schema class may be used to update existing tables. Like the create method, the table method accepts two arguments: the name of the table and a Closure that receives a Blueprint instance you may use to add columns to the table:

```php
Schema::table('users', function (Blueprint $table) {
    $table->string('email');
}, "connection");
```

### Available Column Types

| Command | Description |
| --- | --- |
| `$table->bigIncrements('id');` | Auto-incrementing UNSIGNED BIGINT (primary key) equivalent column. |
| `$table->bigInteger('votes');` | BIGINT equivalent column. |
| `$table->binary('data');` | BLOB equivalent column. |
| `$table->boolean('confirmed');` | BOOLEAN equivalent column. |
| `$table->char('name', 100);` | CHAR equivalent column with an optional length. |
| `$table->date('created_at');` | DATE equivalent column. |
| `$table->dateTime('created_at');` | DATETIME equivalent column. |
| `$table->decimal('amount', 8, 2);` | DECIMAL equivalent column with a precision (total digits) and scale (decimal digits). |
| `$table->double('amount', 8, 2);` | DOUBLE equivalent column with a precision (total digits) and scale (decimal digits). |
| `$table->char('name', 100);` | CHAR equivalent column with an optional length. |
| `$table->float('amount', 8, 2);`|	FLOAT equivalent column with a precision (total digits) and scale (decimal digits). |
| `$table->increments('id');` |	Auto-incrementing UNSIGNED INTEGER (primary key) equivalent column. |
| `$table->integer('votes');` |	INTEGER equivalent column.|
| `$table->mediumInteger('votes');` | MEDIUMINT equivalent column.|
| `$table->string('name', 100);` | VARCHAR equivalent column with a optional length. |
| `$table->text('description');` | TEXT equivalent column. |
| `$table->time('sunrise');` | TIME equivalent column. |
| `$table->timestamp('added_on');` | TIMESTAMP equivalent column. |
| `$table->timestamps();` |	Adds nullable created_at and updated_at TIMESTAMP equivalent columns. |
| `$table->year('birth_year');` | YEAR equivalent column. |

### Column Modifiers

In addition to the column types listed above, there are several column "modifiers" you may use while adding a column to a database table. For example, to make the column "nullable", you may use the nullable method:

```php
Schema::table('users', function (Blueprint $table) {
    $table->string('email')->nullable();
});
```

| Modifier | Description |
| --- | --- |
| `->autoIncrement()` | Set INTEGER columns as auto-increment (primary key) | 
| `->comment('my comment')` | Add a comment to a column (MySQL/PostgreSQL) |
| `->default($value)` |	Specify a "default" value for the column |
| `->nullable()` |	Allows (by default) NULL values to be inserted into the column |
| `->unique()` | Adds UNIQUE key word to field |
