# Database: Migrations

 - [Introduction](#introduction)
 - [Generating Migrations](#)
 - [Migration Structure](#)
 - [Running Migrations](#)
 - [Tables](#tables)
 - [](#)

## Introduction

Migrations are like version control for your database, allowing your team to easily modify and share the application's database schema.

## Generating Migrations


To create a migration, use the `make:migration` Framy Command.

```
php Framy make:migration users_table
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
| `$table->increments('id');` |	Auto-incrementing UNSIGNED INTEGER (primary key) equivalent column. |
| `$table->string('name', 100);` | VARCHAR equivalent column with a optional length. |
| `$table->text('description');` | TEXT equivalent column. |
| `$table->time('sunrise');` | TIME equivalent column. |
| `$table->timestamp('added_on');` | TIMESTAMP equivalent column. |
| `$table->timestamps();` |	Adds nullable created_at and updated_at TIMESTAMP equivalent columns. |
| `$table->year('birth_year');` | YEAR equivalent column. |
