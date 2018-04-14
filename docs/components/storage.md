# Storage
## Introduction

> Storage Component is a storage abstraction layer that simplifies the way you work with
> files and directories.

## Usage

You will need to use storage drivers to access different storage providers like local disk,
Amazon, Rackspace, etc.

Framy Framework currently provides LocalStorageDriver but using a set of built-in 
interfaces will help you to develop a new driver in no time.
The following driver interfaces are available:

- DriverInterface - main storage driver interface
- TouchableInterface - for drivers that support touch functionality (change of timemodified)

- SizeAwareInterface - for drivers that can access file size
- DirectoryAwareInterface - for drivers that can work with directories
- AbsolutePathInterface - for drivers that can provide absolute file path (ex:/var/www/app/storage/myFile.txt)

## Configuring a storage service

The recommended way of using a storage is by defining a storage service. Here is an
example of defining a service using LocalStorageDriver and S3StorageDriver(this one
only later on): 

NOTE: you can use DIR to have your file paths built dynamically. DIR will be
replaced with the directory path containing current config file.

```php
// inside config/filesystem.php

'disks' => [
    'public' => [
        'driver' => 'local',
        'root' => realpath(__DIR__."/../public"),
        'visibility' => 'public',
    ],
        'templates' => [
        'driver' => 'local',
        'root' => realpath(__DIR__.'/../storage/templates/')
    ],
        'language' => [
        'driver' => 'local',
        'root' => realpath(__DIR__.'/../storage/lang/')
    ]
]
```

## Using your new storage

To make use of local storage easier and more flexible, there are 2 classes:

`\app\framework\Component\Storage\File\File` and
`\app\framework\Component\Storage\Directory\Directory`. These 2 classes serve as
wrappers so you never need to make calls to storage directly. Besides, they contain
common methods you will need to perform actions on files and directories.
Let's take a look at how you would store a new file:

```php
// use StorageTrait
// Get your storage service. Storage name is part of the service name after 'Storage.'
$storage = $this->storage('LocalStorage');

// Create a file object with a key (file name) and a $storage instance
$file = new File('file.txt', $storage);

$contents = file_get_contents(
    'http://www.w3schools.com/images/w3schoolslogoNEW310113.gif'
);

$file->setContents($contents);
```

After calling `setContents($contents)` the contents is written to the storage immediately
and a bool is returned.

## Working with directories

Sometimes you need to read the whole directory, filter files by name, extension, etc. There
is a special interface for this type of manipulation,
`\app\framework\Component\Storage\Directory\DirectoryInterface`.

Since not all storage engines support directories, there is no generic implementation of this
interface. There is, however, an implementation in form of Directory which works nicely
with local file storage. There are 2 modes of reading a directory: recursive and nonrecursive.

- Recursive will read the whole directory structure recursively and build a onedimensional
  array of files (directory objects are not created but their children files
  are returned). This is very useful when you need to read all files at once or filter
  them by name, extension, etc.
- Non-recursive will only read current directory and return both child Directory and
  Fileobjects. You can then loop through child Directory object to go in-depth.

## Reading a directory (non-recursive mode)

```php
// Get your storage service
$storage = $this->storage('LocalStorage');

// Read recursively
$dir = new Directory('2013', $storage, true);

// Get only PDF files
$pdfFiles = $dir->filter('*.pdf');

// Count ZIP files
$zipFiles = $dir->filter('*.zip')->count();

// Get files starting with 'log_'
$logFiles = $dir->filter('log_*');

// You can also pass the result of filter directly to loops as `filter()` returns a new Directory
object
foreach($dir->filter('*.txt') as $file){
    // Do something with your file
}
```

NOTE: calling `filter()` does not change the original Directory object, but creates a new
Directory object with filtered result, so once you've read the root directory you can filter it
using any condition as many times as you need:

```php
// Get your storage service
$storage = $this->storage('LocalStorage');

// Read recursively and don't filter
$dir = new Directory('2013', $storage, true);

// Now you can manipulate the whole directory
// Get number of all ZIP files in the directory tree
$zipFiles = $dir->filter('*.zip')->count();

// Get number of all RAR files in the directory tree
$zipFiles = $dir->filter('*.rar')->count();

// Get number of all LOG files in the directory tree
$zipFiles = $dir->filter('*.log')->count();

// Now output all files in the directory without filtering them
foreach($dir as $file){
    echo $file->getKey();
}
```

## Filtering files (recursive mode)

To make use of local storage easier and more flexible, there are 2 classes:
`\app\framework\Component\Storage\File\File` and
`\app\framework\Component\Storage\Directory\Directory`. These 2 classes serve as
wrappers so you never need to make calls to storage directly. Besides, they contain
common methods you will need to perform actions on files and directories.
Let's take a look at how you would store a new file:

```php
// use StorageTrait
// Get your storage service. Storage name is part of the service name after 'Storage.'
$storage = $this->storage('LocalStorage');

// Create a file object with a key (file name) and a $storage instance
$file = new File('file.txt', $storage);

$contents = file_get_contents(
    'http://www.w3schools.com/images/w3schoolslogoNEW310113.gif'
);

$file->setContents($contents);
```

After calling `setContents($contents)` the contents is written to the storage immediately
and a bool is returned.

## Deleting a directory

Deleting a directory (this is done recursively) is as simple as:

```php
// Get your storage service
$storage = $this->storage('LocalStorage');

// Get directory
$dir = new Directory('2013', $storage);

// This will delete the whole directory structure and fire FILE_DELETED event for each file along the way
$dir->delete();

// If you don't want the events to be fired, pass as second parameter `false`:
$dir->delete(false);
```

## Storage events
There are 3 types of events fired when certain actions are performed on a File:

- ff.storage.file_saved (StorageEvent::FILE_SAVED) - fired after a file was savedsuccessfully.
- ff.storage.file_renamed StorageEvent::FILE_RENAMED) - fired after a file is renamed.
- ff.storage.file_deleted (StorageEvent::FILE_DELETED) - fired after a file is deleted.

All 3 events pass an instance of `\app\framework\Component\Storage\StorageEvent` to
their event handlers. Once your handler gets executed, you can access the file objects
using `$event->getFile()` method.

```php
class Test
{
    use EventManagerTrait;  

    public function index() {   
        // Listen for StorageEvent::FILE_SAVED
        $this->eventManager()->listen(StorageEvent::FILE_SAVED)->handler(function(StorageEvent $event) {
            // Get the file object
            $file = $event->getFile();
        });
    }
}
```

`StorageEvent::FILE_RENAMED` event also assigns a special property called oldKey to the
event object, which holds the value of file key before renaming (this will help you update
your database records, etc.):