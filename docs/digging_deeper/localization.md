## Introduction

Framy's localization features provide a convenient way to retrieve strings in various languages, allowing you to easily support multiple languages within your application. Language strings are stored in files within the resources/lang directory. Within this directory there should be a subdirectory for each language supported by the application:

```
resources
    \-lang
        \-en
            -messages.php
        \-de
            -messages.php
```

All language files return an array of keyed strings. For example:

```php
return [
    'welcome' => 'Welcome to our application'
];
```

### Configuring The Locale

The default language for your application is stored in the `config/app.php` configuration file. You may modify this value to suit the needs of your application.

You may configure a "fallback language", which will be used when the active language does not contain a given translation string. Like the default language, the fallback language is also configured in the `config/app.php` configuration file:

```
'fallback_locale' => 'en',
```

### Determining The Current Locale

```php
$local = Trans::getLocale();

if (Trans::isLocale('en')) {
    //
}
```

## Defining Translation Strings

In the `resources/lang` directory are the locales located. Example:

```
resources
    \-lang
        \-en
            -messages.php
        \-de
            -messages.php
```

----

`resources/lang/en/messages.php`:
```php
<?php

return [
    "welcome" => "Welcome to our application"
];
```
`resources/lang/en/messages.php`:
```php
<?php

return [
    "welcome" => "Willkommen zu unserer Anwendung",
];
```

In the example above we have defined the message strings for english and german (de - deutsch) how you name the lang folder (e.g. "en") does't matter because only you will work with it. We suggest using the 2 letter shortage for the countries.

## Retrieving Translation Strings

In general: 

```php
Trans::get("messages.welcome");
```

In templates:

```smarty
{trans k="messages.welcome"}
```