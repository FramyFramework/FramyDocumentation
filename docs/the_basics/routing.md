# Routing

- [Getting Started](#getting-started)
- [Examples](#examples)
- [Api](#api)
    - [$request methods:](#request-methods)
    - [$response methods:](#response-methods)
- [Routing](#routing)

## Getting Started

All the routes are located in the `routes/web.php` file.

## Examples

Hello World - Obligatory hello world example

```php
use app\framework\Component\Routing\Router;

Router::get("/", function () {
    return "Hello World";
});
```

You can also pass a method of your controller. Here:

 ```php
 use app\framework\Component\Routing\Router;
 
 // <class_name>@<method_name>
 Router::get("/", "ExampleController@HelloWorld");
 ```
## Api
Create a route with e.g. `get($route, $callback)` or `post($route, $callback)` where callback is `function ($request, $response)`

Below is a list of the public methods in the common classes you will most likely use.

### $request methods:

| Method | Description |
|---|---|
| header($key)                      |Gets a request header |
| cookie($key)                      |Gets a cookie from the request |
| session($key)                     |Gets a session variable |
| param($key, $default = null)      |Gets a request parameter (get, post, named) |
| params()                          |Return all parameters |
| params($mask = null)              |Return all parameters that match the mask array - extract() friendly |
| validate($param, $err_msg = null) |Starts a validator chain |
| method()                          |Gets the request method |
| method($method)                   |Checks if the request method is $method, i.e. method('post') => true |
| isSecure($required = false)       |https? Redirect if $required is true and the request is not secure |
| id()                              |Gets a unique ID for the request |
| ip()                              |Get the request IP |
| userAgent()                       |Get the request user agent |
| uri()                             |Get the request URI |
| <property>                        |Gets a request parameter |

### $response methods:

| Method | Description |
|---|---|
| header($key, $value = null)                   | Sets a response header |
| cookie($key, $value = null, $expiry = null)   | Sets a cookie |
| cookie($key, null)                            | Removes a cookie |
| flash($msg, $type = 'info', $params = array() | Sets a flash message |
| file($file, $filename = null)                 | Send a file |
| json($object, $callback = null)               | Send an object as JSON(p) |
| markdown($str, $args, ...)                    | Return a string formatted with markdown |
| code($code)                                   | Sends an HTTP response code |
| redirect($url, $code = 302)                   | Redirect to the specified URL |
| refresh()                                     | Redirect to the current URL |
| back()                                        | Redirect to the referer |
| render($view, $data = array())                | Renders a view or partial (NOTE: in the scope of $response) |
| layout($layout)                               | Sets the view layout |
| yieldView()                                   | Call inside the layout to render the view content |
| onError($callback)                            | $callback takes ($response, $msg, $err_type = null) |
| set($key, $value = null)                      |  | 
| set($arr)                                     | Set a view property or helper |
| escape($str)                                  | Escapes a string |
| query($key, $value = null)                    |  |
| query($arr)                                   | Modify the current query string |
| param($param, $default = null)                | Gets an escaped request parameter |
| flashes($type = null)                         | Retrieves and clears all flashes of $type (or all flash messages) |
| flush()                                       | Flush all open output buffers |
| discard()                                     | Discard all open output buffers |
| buffer()                                      | Return the contents of the output buffer as a string |
| dump($obj)                                    | Dump an object |
| chunk($str = null)                            | Enable response chunking (see the wiki) |
| {callback} ($arg1, ...)                       | Calls a user-defined helper |
| {property}                                    | Gets a user-defined property |

## Routing

Syntax:

`[ match_type : param_name ]`

Some examples
```
*                    // Match all request URIs
[i]                  // Match an integer
[i:id]               // Match an integer as 'id'
[a:action]           // Match alphanumeric characters as 'action'
[h:key]              // Match hexadecimal characters as 'key'
[:action]            // Match anything up to the next / or end of the URI as 'action'
[create|edit:action] // Match either 'create' or 'edit' as 'action'
[*]                  // Catch all (lazy)
[*:trailing]         // Catch all as 'trailing' (lazy)
[**:trailing]        // Catch all (possessive - will match the rest of the URI)
.[:format]?          // Match an optional parameter 'format' - a / or . before the block is also optional
```
Some more complicated examples
```
/posts/[*:title][i:id]     // Matches "/posts/this-is-a-title-123"
/output.[xml|json:format]? // Matches "/output", "output.xml", "output.json"
/[:controller]?/[:action]? // Matches the typical /controller/action format
```