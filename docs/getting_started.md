# Getting started

This is the official documentation from probably the badest PHP Framework ever. Framy!
The Ugly little brother from Laravel, Symfony and other good frameworks.
Have fun or what ever ¯\_(ツ)_/¯

## Setup

You can easily setup Framy by copying its data to your Apache folder. There is no further
installation or setup by Framy needed. This still requires an Apache and MySQL server.

## Requirements

The Framy framework has only a few system requirements.
 - PHP >= 7.0.0
 - PDO PHP Extension
 - MySQL

## Configuration
### Public Directory

After installing Framy you should configure your web server's document / web root to be
the **public** directory. The **index.php** in this directory serves as the front controller for all
HTTP requests entering your application.

### Configuration files

All the configuration files are stored in the config directory. Each option is documented, so
feel free to look through the files and get familiar with the options available to you.

### Directory permissions

After configuring Framy you may need to set up some permissions. Framy needs in the
Storage directory writeable otherwise your web server will not run.

### CrypKey

You should change the CrypKey in `config/app.php` an random string. Typically, this string
should be 32 characters long.
**If the application key is not set, your user sessions and other encrypted data will
not be secure!**

### Database connection

If you want a database connection you will need to configure it in the
**config/database.php** file. It comes with an example where you just need to copy&paste
you Information, also Framy can Handle multiple connections, if you want that you can
simply copy&paste the hole block and just need to change the name to make the 
connection work.

### Additional configuration

Framy needs almost no other configuration out of the box. You are free to get started
developing! However, you may wish to review the **config/app.php** file and its
documentation. It contains several options such as *timezone* and locale that you may wish
to change according to your application.