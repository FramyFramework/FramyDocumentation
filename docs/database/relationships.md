# Relationships

- [Introduction](#introduction)

## Introduction

Database tables are often related to one another. For example, a blog post may have many comments, or an order could be related to the user who placed it. Framy supports several types of relationships.

 - One To One
 - One To Many
 - Many To Many
 
 ## Defining Relationships
 
 Relationships are defined as methods on your model classes. They also serve as powerful query builders, defining relationships as methods provides powerful method chaining and querying capabilities
 
 ### One To One
 
A one-to-one relationship is a very basic relation. For example, a User model might be associated with one Phone. To define this relationship, we place a phone method on the  User model. The phone method should call the hasOne method and return its result:
 
 ```php
<?php
namespace App;

use app\framework\Component\Database\Model\Model;

class User extends Model
{
    /**
    * Get the phone record associated with the user.
    */
    public function phone()
    {
        return $this->hasOne('App\Phone');
    }
}
```