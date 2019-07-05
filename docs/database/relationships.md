# Relationships

- [Introduction](#introduction)
- [Defining Relationships](#defining-relationships)
    - [One To One](#one-to-one)
        - [Defining The Inverse Of The Relationship](#defining-the-inverse-of-the-relationship)
    - [One to Many](#one-to-many)
    - [One to Many (inverse)](#one-to-many-inverse)
- [Querying Relations](#querying-relations)

## Introduction

Database tables are often related to one another. For example, a blog post may have many comments, or an order could be related to the user who placed it. Framy supports several types of relationships.


 - [One To One](#one-to-one)
 - [One to Many](#one-to-many)
 - Many To Many
 
## Defining Relationships
 
Relationships are defined as methods on your model classes. They also serve as powerful query builders, defining relationships as methods provides powerful method chaining and querying capabilities
 
### One To One

A one-to-one relationship is a very basic relation. For example, a User model might be associated with one Phone. To define this relationship, we place a phone method on the  User model. The phone method should call the hasOne method and return its result:
 
 ```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class User extends Model
{
    /**
     * Get the phone record associated with the user.
     */
    public function phone()
    {
        return $this->hasOne(Phone::class);
    }
}
```

Framy determines the foreign key of the relationship based on the model name. In this case, the `Phone` model is automatically assumed to have a `user_id` foreign key. If you wish to override this convention, you may pass a second argument to the `hasOne` method:

```php
return $this->hasOne('App\Phone', 'foreign_key');
```

Additionally, Framy assumes that the foreign key should have a value matching the `id` (or the custom `$primaryKey`) column of the parent. In other words, Framy will look for the value of the user's `id` column in the `user_id` column of the `Phone` record. If you would like the relationship to use a value other than `id`, you may pass a third argument to the `hasOne` method specifying your custom key:

return $this->hasOne('App\Phone', 'foreign_key', 'local_key');

#### Defining The Inverse Of The Relationship

So, we can access the `Phone` model from our `User`. Now, let's define a relationship on the  `Phone` model that will let us access the `User` that owns the phone. We can define the inverse of a `hasOne` relationship using the `belongsTo` method:

 ```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class Phone extends Model
{
    /**
     * Get the user that owns the phone.
     */
    public function user()
    {
        return $this->belongsTo(User::class);
    }
}
```

In the example above, Framy will try to match the `user_id` from the `Phone` model to an `id` on the `User` model. Framy determines the default foreign key name by examining the name of the relationship method and suffixing the method name with `_id`. However, if the foreign key on the `Phone` model is not `user_id`, you may pass a custom key name as the second argument to the `belongsTo` method:

```php
/**
 * Get the user that owns the phone.
 */
public function user()
{
    return $this->belongsTo(User::class, 'foreign_key');
}
```

If your parent model does not use `id` as its primary key, or you wish to join the child model to a different column, you may pass a third argument to the `belongsTo` method specifying your parent table's custom key:

```php
/**
 * Get the user that owns the phone.
 */
public function user()
{
    return $this->belongsTo(User::class, 'foreign_key', 'other_key');
}
```

### One To Many

A one-to-many relationship is used to define relationships where a single model owns any amount of other models. For example, a blog post may have an infinite number of comments. Like all other database relationships, one-to-many relationships are defined by placing a function on your model class:

```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class Post extends Model
{
    /**
     * Get the comments for the blog post.
     */
    public function comments()
    {
        return $this->hasMany(Comment::class);
    }
}
```

Remember, Framy will automatically determine the proper foreign key column on the `Comment` model. By convention, Framy will take the "snake case" name of the owning model and suffix it with `_id`. So, for this example, Framy will assume the foreign key on the `Comment` model is `post_id`.

Since all relationships also serve as query builders, you can add further constraints to which comments are retrieved by calling the `comments` method and continuing to chain conditions onto the query:

```php
$comment = App\Post::find(1)->comments()->where('title', 'foo')->first();
```

Like the `hasOne` method, you may also override the foreign and local keys by passing additional arguments to the `hasMany` method:

```php
return $this->hasMany('App\Comment', 'foreign_key');

return $this->hasMany('App\Comment', 'foreign_key', 'local_key');
```

### One To Many (Inverse)

Now that we can access all of a post's comments, let's define a relationship to allow a comment to access its parent post. To define the inverse of a `hasMany` relationship, define a relationship function on the child model which calls the `belongsTo` method:

```php
<?php
namespace App;

use app\framework\Component\Database\Model\Model;

class Comment extends Model
{
    /**
     * Get the post that owns the comment.
     */
    public function post()
    {
        return $this->belongsTo('App\Post');
    }
}
```

In the example above, Framy will try to match the `post_id` from the `Comment` model to an  `id` on the `Post` model. Framy determines the default foreign key name by examining the name of the relationship method and suffixing the method name with a `_` followed by the name of the primary key column. However, if the foreign key on the `Comment` model is not  `post_id`, you may pass a custom key name as the second argument to the `belongsTo` method:

```php
/**
 * Get the post that owns the comment.
 */
public function post()
{
    return $this->belongsTo(Post::class, 'foreign_key');
}
```

If your parent model does not use `id` as its primary key, or you wish to join the child model to a different column, you may pass a third argument to the `belongsTo` method specifying your parent table's custom key:

```php
/**
 * Get the post that owns the comment.
 */
public function post()
{
    return $this->belongsTo(Post::class, 'foreign_key', 'other_key');
}
```

## Querying Relations

Since all of the relationships are defined in methods, you may call these methods to obtain an instance of the relationship without actually executing the relationship queries. In addition all relationships serve as [QueryBuilder](query_builder.md), allowing you to continue to chain constrains onto the relationship query before finally executing the SQL against the database.

For example imagine a blog system in which a User has manny related posts:

```php
<?php
namespace app\custom\Models;

use app\framework\Component\Database\Model\Model;

class User extends Model
{
    public function posts()
    {
        return $this->hasMany(Post::class);
    }
}
```

You may query the posts relationship and add additional constraints to the relationship like so:

```php
$user = User::find(1);

$user->posts()->get();
```

You are able to use any of the [QueryBuilder](query_builder.md) methods on the relationship, so be sure to explore the query builder documentation to learn about all of the methods that are available to you.