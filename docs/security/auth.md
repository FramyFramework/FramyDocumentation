# Authentication

## Introduction

Framy provides an basic User Authentication out of the box. With everything you might need. Since all applications are different from each other you can change all of it to your needs.

## Database

The `CreateUseresTaple.php` file located at `database/migrations` contains as the name says the migration class for the users table in the database. So all you have to do is run the `php Framy migrate` command. You are free to edit it to your needs.

## AuthController

The AuthController manages all the Auth stuff. everything you see in there right away is well documented and you are free to edit it to your needs.

## Template

You can simply access the `Auth` Class, with all its functionality via the `$auth` value from inside the templates.