# Stopwatch

 - [Introduction](#introduction)
 - [Usage](#usage)
 - [Periods](#periods)
 - [Sections](#sections)

## Introduction

The Stopwatch component provides a way to profile code.

## Usage

The Stopwatch component provides an easy and consistent way to measure execution
time of certain parts of code so that you don't constantly have to parse micro time by
yourself. Instead, use the simple Stopwatch class:

```php
use app\framework\Component\Stopwatch\Stopwatch;
$stopwatch = new Stopwatch();
// Start event named 'eventName'
$stopwatch->start('eventName');
// ... some code goes here
$event = $stopwatch->stop('eventName');
```

The `StopwatchEvent` object can be retrieved from the `start()`, `stop()`, `lap()` and `getEvent()`
methods. The latter should be used when you need to retrieve the duration of an event
while it is still running.
You can also provide a category name to an event:

```php
$stopwatch->start('eventName', 'categoryName');
```

You can consider categories as a way of tagging events. For example, the Framy Profiler
tool uses categories to nicely color-code different events.

## Periods

As you know from the real world, all stopwatches come with two buttons: one to start and
stop the stopwatch, and another to measure the lap time. This is exactly what the `lap()`
method does:

```php
$stopwatch = new Stopwatch();
// Start event named 'foo'
$stopwatch->start('foo');
// ... some code goes here
$stopwatch->lap('foo');
// ... some code goes here
$stopwatch->lap('foo');
// ... some other code goes here
$event = $stopwatch->stop('foo');
```

Lap information is stored as "periods" within the event. To get lap information call:

```php
$event->getPeriods();
```

In addition to periods, you can get other useful information from the event object. For
example:

```php
$event->getCategory();   // Returns the category the event was started in
$event->getOrigin();     // Returns the event start time in milliseconds
$event->ensureStopped(); // Stops all periods not already stopped
$event->getStartTime();  // Returns the start time of the very first period
$event->getEndTime();    // Returns the end time of the very last period
$event->getDuration();   // Returns the event duration, including all periods
$event->getMemory();     // Returns the max memory usage of all periods
```

## Sections

Sections are a way to logically split the timeline into groups. You can see how Framy uses
sections to nicely visualize the framework life cycle in the Framy Profiler tool. Here is a
basic usage example using sections:

```php
$stopwatch = new Stopwatch();
$stopwatch->openSection();
$stopwatch->start('parsing_config_file', 'filesystem_operations');
$stopwatch->stopSection('routing');
$events = $stopwatch->getSectionEvents('routing');
```

You can reopen a closed section by calling the `openSection()` method and specifying the id
of the section to be reopened:

```php
$stopwatch->openSection('routing');
$stopwatch->start('building_config_tree');
$stopwatch->stopSection('routing');
```