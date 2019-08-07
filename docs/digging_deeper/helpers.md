# Helpers

 - [Introduction](#introduction)
 - [Available Methods](#available-methods)
 - [Method Listing](#method-listing)

## Introduction

Framy provides some global "Helper" PHP functions. Most of them are used by the framework but feel free to use them as well. 

## Available Methods

| URLs |
|---|
| [url](#url) |

| Paths |
|---|
| [pathTo](#pathto) |

| String |
|---|
| [getStringBetween](#getstringbetween) |
| [str](#str)

| Miscellaneous |   
|---|
| [app](#app) |
| [dd](#dd) |
| [view](#view) |
| [get_connection_log](#get_connection_log)

## Method Listing
### URLs
#### url

Basically completes just the the url
e.g. /test to yourexample.site/test

Simple, very simple.

```php
url($path);
```
### Paths
#### pathTo

Easy function to get the path to the project + if you want an directory in it.

```php
pathTo($pathInProject);
```

### String
#### getStringBetween

This is a handy little function to strip out a string between
two specified pieces of text. This could be used to parse
XML text, bbCode, or any other delimited code/text for that matter.

#### str

StringObject

### Miscellaneous
#### app

Used to easily call Methods from classes without manually set locally Instances of them.

```php
app($classMethod, $param);
```

#### dd

The `dd` function dumps the given variables and ends execution of the script:

```php
dd($value);
``` 

#### view

Get the evaluated view contents for the given view.

```php
view($templateName, $dataForTemplate);
```

#### get_connection_log

returns query log from Connection as array

```php
get_connection_log();
```