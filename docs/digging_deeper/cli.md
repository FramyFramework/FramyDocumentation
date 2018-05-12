# Framy Console
## Introduction
Framy provides an Command-Line-Interface with an small number of default commands which can help you while building your application.

To use this you will need to navigate in your console to the root directory of your project.
To view a list of all available Framy commands, you may use the `list` command.

```
php Framy list
```

Every command also includes a "help" screen which displays and describes the command's available arguments and options. To view a help screen, precede the name of the command with `help`:

```
php Framy help new-command
```

## Writing Commands

In addition to the commands provided with Framy, you may also build your own custom commands. Commands are typically stored in the `app/custom/Console` directory.

## Generating Commands

To create a new command, use the `new-command` Framy command. This command will create a new command class in the `app/custom/Console` directory. The generated command will include the default set of properties and methods that are present on all commands:

```
php Framy new-command CommandName
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
- `Command::REQUIRED`
- `Command::OPTIONAL`
- `Command::IS_ARRAY`

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
- `Command::VALUE_NONE` 
- `Command::VALUE_REQUIRED` 
- `Command::VALUE_OPTIONAL` 
- `Command::VALUE_IS_ARRAY` 