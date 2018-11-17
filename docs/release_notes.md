# Version 0

## v0.3.2 - 2018-11-17

- **Added**: Better exception handling in `app\framework\Component\App\App`
- **Added**: Handling in case value is not an array 
- **Changed**: `$param` argument in `app()` helper function has now empty array as default. What fixed some issues/warnings with that.
- **Fixed**: unhandled exceptions in `app\framework\Component\App\App`
- **Fixed**: Value in ArrayObject is null if null is given #11


## v0.3.1

- **Removed**: middleware directory
- **New**: Implemented new exception system mostly everywhere
- **Fix**: Issue with wrong namespace in Make Commands templates
- **Fix**: Fixed issue with View

## v0.3

- **New**: Added possibility to use Directory without needing an Disk
- **New**: Added helper function `handle()` to handle Exceptions
- **New**: Debug mode
- **New**: added latest version of css Framework Bootstrap to public dir.
- **New**: added more types in Blueprint

## v0.2.3

 - **Fix** I am an idiot. (forgot to change versions in config files)

## v0.2.2

 - **Fix**: missing `templates_c` folder

## v0.2.1

 - **Fix**: Issue #2 - `Undefined index: driver` warning should not appear anymore  
 - **Fix**: Issue #1 - Spelling of an link in the welcome template
 - **New**: Commands can now be stored in the Component. And are registered via namespace 
 - **New**: [Database: Migrations](database/migration.md)

## v0.2.0

- **Fix**: The Storage Comp. had some weird issues
- **New**: Console Comp. Commands with custom usability can be added now
- **New**: Resource directory. For Compiled files like .sass etc.
- **New**: Structure in Storage directory
- I moved the code to another GitHub repository because that's cleaner

## v0.1.4

- **Fix**: In some files were an mispronunciation of Framy
- **Fix**: Removed some unnecessary files
- **New**: Documentation and API Reference files

## v0.1.3.2

- **Fix**: helper function app() default namespaces had wrong spelling
- **Fix**: little fetch issue in view
- **New**: helper function pathTo() gives the path to the project and adds the possibility to add some path

## v0.1.3.1

- I am an stupid moron

## v0.1.3

- **New**: Cookie comp.
- **Fix**: Issue #12, #13, #14

## v0.1.2

- **New**: Fetch support for View comp.

## v0.1.1

- **New**: Added EventManagerTrait for Model Comp.

## v0.1.0

- **New**: Moved bootstrap file in to bootstrap folder and exported helper in to a separate file
- **New**: start page template
- **New**: helper function app, to call methods and store the class instance.
- **New**: helper function url, to get the URL completely by only entering shit like: /test to example.com/test
- **Fix**: Spelling correction

## v0.1.0-alpha.3

- **New**: Changed the View Comp. you can now edit template path and compile template path in an new config file (view)
- **New**: version available in app config file
- **Fix**: resolved some issues: like an missing semicolon.
- **Fix(kind of)**: some shitty clean up work, like remove empty spaces.

## v0.1.0-alpha.2

- **New**: Model component
- **New**: View comp.
- Changed Database comp.
- Made the Code a little more beautiful
- maybe more I forgot about

## v0.1.0-alpha.1

- init version
