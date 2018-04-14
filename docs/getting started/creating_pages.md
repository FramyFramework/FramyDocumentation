# Creating Pages

Quite at first you should register the route. You can read how to exactly do this under
Routing. But here an example:

```php
$klein->respond("GET", "/", function(){
    view("welcome");
});
```

Inside the function can everything happen like calling an method from an class. In this
example we will not do this.

We will just use the `view()` helper function and display the "welcome" template
To do this we need to add an Template. Lets name it `welcome.tpl` (.tpl ending -> syntax
Smarty requires).

We add the file under `storage/templates`.
`welcome.tpl` shall look like this:

```html
<head>
    <title>Framy</title>
</head>
<body>
    <div class="flex-center position-ref full-height">
        <div class="content">
        <div class="title m-b-md">
            Framy
        </div>
        </div>
    </div>
</body>
</html>
```