# Middleware

- [Introduction](#introduction)
- [Defining Middleware](#defining-middleware)
- [Registering Middleware](#registering-middleware)
    - [Global Middleware](#global-middleware)
    - [Assigning Middleware To Routes](#assigning-middleware-to-routes)
    - [Middleware Groups](#middleware-groups)

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

### Global Middleware
### Assigning Middleware To Routes
### Middleware Groups