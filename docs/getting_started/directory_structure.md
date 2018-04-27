# Directory Structure
## Introduction

The default Framy application structure is intended to provide a great starting point for
both large and small applications. Of course, you are free to organize your application
however you like. Framy imposes almost no restrictions on where any given class is
located.

## The Root Directory

In the root directory is every file of the project and Framy.

## The app Directory

Inside the **app** directory, as you might expect, are all the core Class of your code and
Framys. However especially for you its required to know that specially folder custom is for
you. Because you are Special. Happy Birthday.

### The config Directory

The config directory, as the name implies, contains all the config files. It's a great idea
toread through all of these files and familiarize yourself with all of the options available to
you.

### The public Directory

The **public** directory contains the **index.php** file, which is the entry point for all requests
entering your application. This directory also houses your assets such as images,
JavaScript, and CSS.

### The routes Directory

The routes directory contains the files **web.php** and **api.php**. Where you register the web
an api routes.

### The storage Directory

The storage directory contains your views as well as your raw, un-compiled assets such as
LESS, SASS, or JavaScript. This directory also houses all of your language files and
everything else you want to store.

### The App Directory

The **app** Directory which contains the core code of Framy. And your code, in the custom
directory. For further information about the core code see **Framy API Reference**.