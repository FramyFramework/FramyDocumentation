# Views

 - [Usage](#usage)
 - [Extra features](#extra-features)

## Usage

With the awesome helper function view you can display your views extremely simple:

```php
view("welcome");
//or view("welcome.tpl") both works but the file itself must have .tpl as ending
```

Shows the `view.tpl` file inside the pre defined template disk. If you want to use sub
directory's, you can do that but you need to type them in like this:

```php
view("sub/dir/yourview");
```

## Extra features

You can assign data to Smarty values by simply adding it as an array parameter:

```php
view("yourTemplate", ["valueName" => "someValuedataThatCouldBeAnythingYouWant"]);
```

You can add as many as you want.
You can even assign rendered templates to values:

```php
view("yourTemplate", ["valueName" => "fetch:someTemplate"]);
```