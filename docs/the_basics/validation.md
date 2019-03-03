# Validation

- [Introduction](#introduction)
- [Usage](#usage)
- [Default validators](#default-validators)

## Introduction

Framy got out of the box a validation component with a lot of validator as default.

## Usage

Simply use the `ValidationTrait` where ever you need it.

```php
class HomeController
{
    use ValidationTrait;
    
    public function index()
    {
        // is required and must be at least 12 chars long 
        $this->validate($text, "required, min:12")
    }
}
```

## Default validators

- Email
- URL
- Number
- Integer
- IP
- Required
- MacAddress
- Phone
- Password
- GreaterThan
- GreaterThanOrEqual
- LessThan
- LessThanOrEqual
- MinLength
- MaxLength
- CreditCardNumber
- GeoLocation