# Smart Home Refactoring C++ Kata

[![CI](https://github.com/Coding-Cuddles/smart-home-refactoring-cpp-kata/actions/workflows/main.yml/badge.svg)](https://github.com/Coding-Cuddles/smart-home-refactoring-cpp-kata/actions/workflows/main.yml)
[![Replit](https://replit.com/badge?caption=Try%20with%20Replit&variant=small)](https://replit.com/new/github/Coding-Cuddles/smart-home-refactoring-cpp-kata)

## Overview

This kata complements [Clean Code: SOLID, Ep. 13 - Dependency Inversion Principle](https://cleancoders.com/episode/clean-code-episode-13).

In this exercise, you'll practice refactoring code to adhere to the Dependency
Inversion Principle (DIP). You'll be working with a smart home system that
controls different types of lights and an air conditioner.

## Instructions

### Exercise 1

The initial code consists of several device classes and the
`SmartHomeController` class, which is responsible for controlling all the
devices (lights and air conditioner).

However, the initial code violates the Dependency Inversion Principle, as the
`SmartHomeController` class directly depends on concrete classes. In the tests,
we also directly manipulate the `dimmable_light` and `networkable_light`
instances to check their unique behaviors.

Your goal is to refactor the code to adhere to the Dependency Inversion
Principle and make it easier to implement new devices.

Here are some guidelines to follow:

1. Introduce an interface or several interfaces (or abstract base classes) for
   the devices that the `SmartHomeController` interacts with.

1. Update the `SmartHomeController` class to depend on this interface, instead
   of the concrete device classes.

1. Update the devices to implement these interfaces.

1. Modify any constructors or method calls as necessary to accommodate the
   refactoring.

> **Note**
>
> Remember that in this exercise, we assume all devices are in an ideal state
> and don't account for error cases such as a network connection failure or an
> attempt to dim a light below 0% or above 100% brightness.

Make sure the program still behaves the same way after your refactoring.
There's a unit test in place that checks that on a very rudimentary level by
just looking at the output of the program.

### Exercise 2

When you're done with refactoring, test the quality of your refactoring by
implementing two additional scenarios (methods) in `SmartHomeController`:

1. Add the `make_quick_breakfast` scenario to open the blinds and make a
   predefined coffee type.
   1. Add `Blinds` device class with `open` and `close` methods
      (blinds are always powered and does not have on/off function).
   1. Add `make_quick_breakfast` method to `SmartHomeController`.

1. Add automatic vacuum cleaner and the `schedule_night_cleaning` scenario, which
   should start the cleaning once everything else is turned off.
   1. Add `VacuumCleaner` device class with `start_cleaning` and `stop_cleaning`
      methods.
   1. Add `schedule_night_cleaning` method to `SmartHomeController`. After
      calling this method, the vacuum cleaner should start cleaning once all
      other devices are turned off.

Evaluate whether or not your refactoring made life easier for you, or not.

## Usage

You can import this project into [Replit](https://replit.com), and it will
handle all dependencies automatically.

### Prerequisites

* [CMake 3.19+](https://cmake.org)
* [Ninja](https://ninja-build.org)
* [GTest](https://github.com/google/googletest)

### Build

```console
make
```

### Run main

```console
make run
```

### Run tests

```console
make test
```
