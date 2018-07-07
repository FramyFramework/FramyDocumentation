# Framy Console

 - [Introduction](#introduction)
 - [Writing Commands](#writing-commands)
 - [Creating a Command](#creating-a-command)
 - [Configuring the Command](#configuring-the-command)
 - [Generating Commands](#generating-commands)
 - [Console Output](#console-output)
 - [Defining Input Expectations](#defining-input-expectations)
    - [Arguments](#arguments)
    - [Options](#options)
 - [Color and Style the Output](#color-and-style-the-output)
    - [Using Color Styles](#using-color-styles)

## Introduction
Framy provides an Command-Line-Interface with an small number of default commands which can help you while building your application.

To use this you will need to navigate in your console to the root directory of your project.
To view a list of all available Framy commands, you may use the `list` command.

```
php Framy list
```

Every command also includes a "help" screen which displays and describes the command's available arguments and options. To view a help screen, precede the name of the command with `help`:

```
php Framy help make:command
```

## Writing Commands

In addition to the commands provided with Framy, you may also build your own custom commands. Commands are typically stored in the `app/custom/Console` directory.

## Creating a Command
   
Commands are defined in classes extending Command. For example, you may want a command to create a user:

```php
class CreateUserCommand extends Command
{
    protected function configure()
    {
        // ...
    }

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        // ...
    }
}
```

## Configuring the Command
   
First of all, you must configure the name of the command in the configure() method. Then you can optionally define a help message and the input options and arguments:
   
```php   
// ...
protected function configure()
{
   $this
       // the name of the command
       ->setName('app:create-user')
   
       // the short description shown while running "php bin/console list"
       ->setDescription('Creates a new user.')
   
       // the full command description shown when running the command with
       // the "--help" option
       ->setHelp('This command allows you to create a user...')
   ;
}
```

## Generating Commands

To create a new command, use the `make:command` Framy command. This command will create a new command class in the `app/custom/Console` directory. The generated command will include the default set of properties and methods that are present on all commands:

```
php Framy make:command CommandName
```

## Console Output
  
The execute() method has access to the output stream to write messages to the console:

```php
// ...
protected function execute(InputInterface $input, OutputInterface $output)
{
    // outputs multiple lines to the console (adding "\n" at the end of each line)
    $output->writeln([
        'User Creator',
        '============',
        '',
    ]);

    // the value returned by someMethod() can be an iterator (https://secure.php.net/iterator)
    // that generates and returns the messages with the 'yield' PHP keyword
    $output->writeln($this->someMethod());

    // outputs a message followed by a "\n"
    $output->writeln('Whoa!');

    // outputs a message without adding a "\n" at the end of the line
    $output->write('You are about to ');
    $output->write('create a user.');
}
```

## Defining Input Expectations

When writing console commands, it is common to gather input from the user through arguments or options.
Framy provides this via using the `$this->setDefinition()` method in `configure()`. As parameter takes `setDefinition()` an instance of `InputDefinition`, which is an wrapper for inputs and options.

Adding Argument's or Option's will be done by giving the `InputDefinition` constructor an array with instance of `InputOption` and `InputArgument`.  

### Arguments

Arguments when given in the array will need some parameter.

```
InputAruments(
   name,        // the name of the input
   mode,        // modes can be seen below
   description, // description of the arguments, required for help view
   default      // default value
)
```

default modes:
- `InputAruments::REQUIRED`
- `InputAruments::OPTIONAL`
- `InputAruments::IS_ARRAY`

except for the name all parameter are optional.

### Options

Just like the Arguments:

```
InputOptions(
    name,           // the name of the input
    shortcut,       // 
    mode,           // modes can be seen below
    description,    // description of the arguments, required for help view
    default         // default value
)
```

default modes:
- `InputOptions::VALUE_NONE`
- `InputOptions::VALUE_REQUIRED`
- `InputOptions::VALUE_OPTIONAL`
- `InputOptions::VALUE_IS_ARRAY`

## Color and Style the Output

By using colors in the command output, you can distinguish different types of output (e.g. important messages, titles, comments, etc.).

### Using Color Styles

Whenever you output text, you can surround the text with tags to color its output. For example:

> By default, the Windows command console doesn't support output coloring.

```php
// green text
$output->writeln('<info>foo</info>');

// yellow text
$output->writeln('<comment>foo</comment>');

// black text on a cyan background
$output->writeln('<question>foo</question>');

// white text on a red background
$output->writeln('<error>foo</error>');
```

The closing tag can be replaced by </>, which revokes all formatting options established by the last opened tag.

You can also set these colors and options directly inside the tag name:

```php
// green text
$output->writeln('<fg=green>foo</>');

// black text on a cyan background
$output->writeln('<fg=black;bg=cyan>foo</>');

// bold text on a yellow background
$output->writeln('<bg=yellow;options=bold>foo</>');

// bold text with underscore
$output->writeln('<options=bold,underscore>foo</>');
```