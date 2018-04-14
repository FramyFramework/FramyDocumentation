# Validation
## introduction

Validation of data means checking that the data provided by the user is in accordance with
the expected format. For example, if you pass the ID of an item in your online shop as a
GET parameter, you should check that this value is actually a number. Good data
validation can significantly increase your protection against SQL injections and cross-site
scripting. 

In addition to the increase in security, a good validation of the input data also provides you
with increased user experience, as incorrect entries are intercepted at an early stage.
In principle, you should check all entries of your users and point out wrong entries by
means of suitable hints. A mistyping of the e-mail address happens quickly and can be
annoying if it is not noticed.

## Usage

Basic Example usage:

```php
Validation::getInstance()->validate('example@web.de', 'email'); // returns true
Validation::getInstance()->validate('false.mail.de', 'email'); // throws Exception
Validation::getInstance()->validate('false.mail.de', 'email', false); // returns "Invalid email"
```

You can either use the example above or use the Validation Trait.

Like this:

```php
use app\framework\Component\Validation\ValidationTrait;

class yourClass
{
    use ValidationTrait;
    
    function yourFunction()
    {
        self::validate()->validate('example@web.de', 'email');
    }
}
```

## General Information

If the given Validators don't mach your requirements, you can add your own by using the
`addValidator()` function.