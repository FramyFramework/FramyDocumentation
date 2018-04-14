# Standard Library
## Introduction

> The Standard Library Component contains some useful functions It's more or less an
> overpowered helper Component

## StdLibTrait & ValidorTrait

Both contain basic functions like `serialize()`, `unserialize()` and basic validators like
`isEmpty()` and many more the usage of them is quite easy and self explaining so no further
explanation needed.

## StdObject

The standard object library is a set of classes that wraps the process of working with some
common objects like arrays, strings, URLs and dates into a objective style (Currently at
version 0.8 just Arrays).
The benefit of working with `StdObject`, instead of native objects, is that you can chain
several methods inside one call which improves the speed how you write your code. The
code is fully objective and we have also "improved" and "fixed" some of the PHP core
functions.
Most of the internal classes inside Framy are written using standard objects.

## ArrayObject

```php
$array = new ArrayObject(['one', 'two', 'three']);
$array->first(); // StringObject 'one'
$array->append('four')->prepend('zero'); // ['zero', 'one', 'two', 'three', 'four']
```

## DateTimeObject

```php
$dt = new DateTimeObject('3 months ago');
echo $dt; // 2013-02-12 17:00:36
$dt->add('10 days')->sub('5 hours'); // 2013-02-22 12:00:36
```

## StringObject

```php
$string = new StringObject('Some test string.');
$string->caseUpper()->trimRight('.')->replace(' test'); // SOME STRING
```

## UrlObject

```php
$url = new UrlObject('http://www.framy.com/');
$url->setPath('search')->setQuery(['q'=>'some string']); // http://www.framy.com/search?
q=some+string
```

The easies and most optimal way to use the StdObject library is by implementing the
`StdObjectTrait`.

```php
class MyClass
{
    use StdObjectTrait;
    public function test() {
        // create StringObject
        $this->str('This is a string');
 
        // create ArrayObject
        $this->arr(['one', 'two']);

        // create UrlObject
        $this->url('http://www.framy.com/');
 
        // create DateTimeObject
        $this->dateTime('now');
    }
}
```