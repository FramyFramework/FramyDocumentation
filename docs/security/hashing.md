# Hashing

## Introduction

You can access the Hashing component with the `Hash` class. It provides secure `Bcrypt` hashing for storing user passwords.

(Bcrypt is a great choice for hashing passwords because its "work factor" is adjustable, which means that the time it takes to generate a hash can be increased as hardware power increases.)

## Configuration

The default hashing driver for your application is configured in the `config/hashing.php` configuration file.

## Basic Usage

You may hash a password by calling the `make` method on the `Hash` class.

```php
$hashedPw = Hash::make($request->password);
``` 

## Verifying A Password Against A Hash

The check method allows you to verify that a given plain-text string corresponds to a given hash.

```php
if (Hash::check('plain-text', $hashedPassword)) {
    // The passwords match...
}
```

## Checking If A Password Needs To Be Rehashed

The needsRehash function allows you to determine if the work factor used by the hasher has changed since the password was hashed:

```php
if (Hash::needsRehash($hashed)) {
    $hashed = Hash::make('plain-text');
}
```
