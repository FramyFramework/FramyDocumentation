# Controller

 - [Introduction](#introduction)
 - [Creating Controller](#creating-controller)

## Introduction

Instead of defining all of your request handling logic as Closures in route files, you may
wish to organize this behaviour using Controller classes. Controllers can group related
request handling logic into a single class. Controllers are stored in the
`app/custom/Http/Controller` directory.

## Creating Controller

You can either create the file in the directory from above by your self or use the `make:controller` command which will 
do the work for you. You can name the controller however you want.