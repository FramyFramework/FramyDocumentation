# Middleware

- [Introduction](#introduction)
- [Defining Middleware](#defining-middleware)
- [Registering Middleware](#registering-middleware)
    - [Global Middleware](#global-middleware)
    - [Middleware Groups](#middleware-groups)
- [Assigning Middleware To Routes](#assigning-middleware-to-routes)

## Introduction

Middleware provides a convenient mechanism for filtering HTTP requests entering your application. For example, Framy includes a middleware that verifies the user of your application is authenticated. If the user is not authenticated, the middleware will redirect the user to the login screen. However, if the user is authenticated, the middleware will allow the request to proceed further into the application.

Additional middleware can be written to perform a variety of tasks besides authentication.  A logging middleware might log all incoming requests to your application.

All of these middleware are located in the app/custom/Http/Middleware directory.

## Defining Middleware

To create a new middleware, use the `make:middleware` Framy command:

`php Framy make:middleware CheckAge`

This command will place a new `CheckAge` class within your `app/custom/Http/Middleware` directory. In this middleware, we will only allow access to the route if the supplied `age` is greater than 200. Otherwise, we will redirect the users back to the `home` URI:

```php
namespace app\custom\Http\Middleware;

use app\framework\Component\Routing\Request;

class CheckAge
{
    /**
     * Handle an incoming request.
     *
     * @param  Request  $request
     */
    public function handle($request)
    {
        if ($request->age <= 200) {
            header("Location: /);
            exit();
        }
    }
}
```

As you can see, if the given `age` is less than or equal to `200`, the middleware will redirect; otherwise, the request will be passed further into the application. To pass the request deeper into the application (allowing the middleware to "pass").

It's best to envision middleware as a series of "layers" HTTP requests must pass through before they hit your application. Each layer can examine the request and even reject it entirely.

## Registering Middleware

The registration of the middleware happens via the `middleware.php` configuration file located in `/config`. If you take a look at that file you can already see the three key elements of the middleware system: global, general and group middleware. They all have comments that roughly explain what they are for and how to configure them. 

Generally a middleware class has to be referenced via fully qualified name: e.g.: `\Some\Class\Name::class`

### Global Middleware
> These middleware are run during every request to your application.

Yep, that is literally what these do, they will be executed with every request without further steps to do.

Here an example on how to configure it:

```php
<?php
return [
    'global' => [
        'middleware_name' => \some\class::class,
        // more middleware's if wanted        
    ]
];
```

*NOTE: Redirects in Global Middleware logic should be handled with care to prevent endless loops a.k.a. To manny redirects errors*

### Middleware

This type of middleware is very similar to the global middleware except that these must be configured in the route. The config is the same except it has the key `middleware` 

```php
<?php
return [
    'middleware' => [
        'middleware_name' => \some\class::class,
        // more middleware's if wanted        
    ]
];
```

### Middleware Groups



## Assigning Middleware To Routes