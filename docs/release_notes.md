# Versioning Scheme

Framy's versioning scheme follows the conventions of [schematic versioning](https://semver.org/)

# Version 0

## v0.11.1 - 2020-02-14

- **Fixed**: Check if Middleware group exists falsely throws an exception and fails - see #67
- **Fixed**: Issue with middleware groups being executed as normal middleware

## v0.11 - 2019-12-18

- **Changed**: class DateTimeObject has been adapted to the general exception handling by removing handle call with just throwing the exception()
- **Changed**: Command "make:migration": connection option is now optional
- **Changed**: Model::freshTimestamp() is now using the datetime helper
- **Changed**: The year in licence File
- **Added**: Method DateTimeObject::diff()
- **Added**: abstract methods val(), keyExists(), count(), isNull(), isInstanceOf(), isArray() in ArrayObject\ManipulationTrait to remove warnings
- **Fixed**: Issue #62 "Updating database entries via Model doesnt work"
- **Fixed**: Indentation of config files. (not really a problem but annoying to look at)
- **Fixed**: Issue #64 "ValidationException not found in Validation Comp."
- **Fixed**: Issue #65 middleware groups now work properly
- **Deprecated**: Query\Builder::isOperatorValid()

## v0.10.1 - 2019-09-14

- **Fixed**: Database: Relation: BelongsToMany: Pivot key relation in the query is now enclosed with "`" see issue #59

## v0.10 - 2019-08-27

- **Changed**: Routing in a way that an exception is shown with more useful trace
- **Changed**: Moved method `Model::getDifference` to ArrayObject as `difference()`
- **Added**: Classloader: Psr4 autoloading standard
- **Added**: Helper function datetime()
- **Added**: Methods to Model class: `query()`, `dot()`, `divide()`, `getKeys()`, `getOnlyValues()`, `isAccessible()`
- **New**: classloader.php configuration file

## v0.9.2 - 2019-08-10

- **Fixed**: Handling "?" markers in query didn't work with multiple markers

## v0.9.1 - 2019-08-09

- **Fixed**: Remove param insertion at Grammar::compileUpdate (see issue #50)
- **Fixed**: Issue with finding changed attributes in Model for Update

## v0.9 - 2019-08-07

- **Added**: Database: Migration: [column modifier](database/migration.md#column-modifiers)
- **Added**: [Middleware](the_basics/middleware.md)
- **Added**: added Middleware config file with default configurations
- **Added**: Database: [Relations](database/relationships.md)
- **Added**: [get_connection_log](digging_deeper/helpers.md#) helper
- **New**: helper function class_basename
- **New**: Storage "middleware" configured
- **Fixed**: Database: Schema: Blueprint created_at & updated_at fields

## v0.8.1 - 2019-05-01

- **Changed**: Cipher key generation command creates now utf-8 encoded string instead of random bytes
- **Changed**: Adapted some DB interaction to new [Query Builder](database/query_builder.md) in Auth component
- **New**: Storage: can now create files
- **Fixed**: Auth: user should get now authenticated after registration
- **Fixed**: Auth: Model::performUpdate() now returns true if anny sets have been updated and false on failure
- **Fixed**: Make commands now work again
- **Fixed**: Abstract Exception formats now messages correctly

## v0.8 - 2019-04-27

- **Changed**: Moved Database Commands in own directory and set it up in CLI Kernel
- **Added**: [Query Builder](database/query_builder.md)
- **Added**: [Model](database/model.md) Basically completely new and now super powerful
- **Added**: Str helper function
- **Added**: `ConnectionNotConfiguredException`
- **New**: method Connection::getNeededModel()
- **New**: method Connection::processInsertGetId()
- **Fixed**: ArrayObject::flatten() was not working properly
- **Fixed**: Too manny connections error: Connection Factory manages connections now in a way that only one instance of conn can ever exist
- **Removed**: $table attribute from Connection::select()

## v0.7 - 2019-03-24

- **New**: Auth component
- **New**: Localization component
- **New**: `rand()` method in StringObject
- **New**: `Http` component now only consisting of an session interaction class 
- **Changed**: Routing to new syntax
- **Changed**: Directory structure
- **Changed**: Template cache dir is now at `/storage/framework/cache/templates/`
- **Added**: Smarty function `trans`
- **Fixed**: No Undefined index warning spamming anymore

## v0.6 - 2019-02-21

- **Fixed**: Issue with firing event
- **Changed**: Database is now firing event on query execution
- **Added**: Helper functions: `version()` and `isDebug()`
- **Added**: Global exception handling by Framy in debug mode 
- **New**: Hashing Component

## v0.5 - 2019-02-13

- **Added**: .editorconfig file
- **Changed**: File indentation
- **Changed**: shorter syntax on using validation trait
- **Changed**: Validation will now actually throw Exceptions
- **New**: [Encryption Component](security/encryption.md)

## v0.4.1 - 2019-02-06

- **Fixed**: "Value must be an array" Exception on firing "ff.database.query_execution" event see #23 
- **Fixed**: Migration works now again -> see #25 
- **New**: Its now possible to only migrate one Migration #26 
- **New**: New command to generate CrypKey #8 
- **Added**: session_start() to bootstrap.php file #24 

## v0.4 - 2019-01-31

- **New**: arr() helper function
- **New**: impode() ArrayObject method
- **New**: map() ArrayObject method
- **New**: DB class with methods to run queries
- **New**: Basic outline for new [Database Component](database/getting_started.md)
- **Deprecated**: I'm working on creating my own Database Component so Medoo will be removed as soon as possible.

## v0.3.3 - 2019-01-05

- **New**: Migrate command tells the user if no migrations exist
- **New**: Migrate command is now telling the user what it does
- **Fixed**: Query\Builder query bug see #19 
- **Fixed**: Some code smells in the helper file (doesn't change anything but makes the code cleaner)

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
