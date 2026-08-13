# Smart home refactoring kata in C++

[![CI](https://github.com/Coding-Cuddles/smart-home-refactoring-cpp-kata/actions/workflows/main.yml/badge.svg)](https://github.com/Coding-Cuddles/smart-home-refactoring-cpp-kata/actions/workflows/main.yml)
[![C++17](https://img.shields.io/badge/C%2B%2B-17-blue.svg)](https://en.cppreference.com/w/cpp/17)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Refactor a smart home controller toward the Dependency Inversion Principle
without changing its behavior. Setup is complete when all four starter tests
pass.

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

1. Update the `SmartHomeController` class to depend on these abstractions
   instead of the concrete device classes.

1. Update the devices to implement these interfaces.

1. Modify any constructors or method calls as necessary to accommodate the
   refactoring.

> [!NOTE]
>
> Remember that in this exercise, we assume all devices are in an ideal state
> and don't account for error cases such as a network connection failure or an
> attempt to dim a light below 0% or above 100% brightness.

Make sure the program still behaves the same way after your refactoring. The
existing tests check this at a rudimentary level by examining the program's
output.

### Exercise 2

When you're done with refactoring, test the quality of your refactoring by
implementing two additional scenarios (methods) in `SmartHomeController`:

1. Add the `make_quick_breakfast` scenario to open the blinds and make a
   predefined coffee type.
   1. Add a `Blinds` device class with `open` and `close` methods
      (blinds are always powered and do not have an on/off function).
   1. Add a `make_quick_breakfast` method to `SmartHomeController`.

1. Add an automatic vacuum cleaner and the `schedule_night_cleaning` scenario,
   which should start cleaning once everything else is turned off.
   1. Add a `VacuumCleaner` device class with `start_cleaning` and
      `stop_cleaning` methods.
   1. Add a `schedule_night_cleaning` method to `SmartHomeController`. After
      calling this method, the vacuum cleaner should start cleaning once all
      other devices are turned off.

Evaluate whether your refactoring made life easier for you or not.

## Prerequisites

Required:

- [Git](https://git-scm.com/downloads)
- A compiler with C++17 support. Choose one:
  - [GCC](https://gcc.gnu.org/) 10+ on Linux
  - [LLVM Clang](https://llvm.org/) 14+ on Linux
  - [Apple Clang](https://developer.apple.com/xcode/) 17+ on macOS
  - [MSVC](https://visualstudio.microsoft.com/) 2022 on Windows
- [CMake 3.24 or later](https://cmake.org)

Optional:

- [GNU Make](https://www.gnu.org/software/make/), for shorter commands. Every
  required task also has direct CMake and CTest commands. Make may be
  unavailable on Windows.

You do not need to install GoogleTest separately. CMake finds an installed
copy or downloads the pinned release when needed.

## Set up the kata

1. Clone the repository:

   ```console
   git clone https://github.com/Coding-Cuddles/smart-home-refactoring-cpp-kata.git
   ```

2. Enter the repository directory:

   ```console
   cd smart-home-refactoring-cpp-kata
   ```

3. Run the starter tests. Use Make when it is installed:

   ```console
   make test
   ```

   Otherwise, use CMake and CTest directly:

   ```console
   cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
   cmake --build build --config Debug
   ctest --test-dir build --build-config Debug --output-on-failure
   ```

The first run may download and build GoogleTest. CTest should report
`100% tests passed`.

If a command reports a missing compiler or CMake, install that prerequisite
and run the setup commands again.

Setup is complete when CTest reports `100% tests passed`.

## Work on the kata

1. Refactor `smart_home.h` while preserving the behavior covered by
   `test_smart_home.cpp`.

2. Run the tests after each change. Use Make when it is installed:

   ```console
   make test
   ```

   Otherwise, use CMake and CTest directly:

   ```console
   cmake --build build --config Debug
   ctest --test-dir build --build-config Debug --output-on-failure
   ```

   Continue when CTest reports `100% tests passed`.

## Make command reference

Make is optional. Run `make` or `make help` to list these commands in the
terminal.

| Command             | Result                                    |
| ------------------- | ----------------------------------------- |
| `make all`          | Build and run the test suite              |
| `make help`         | Show the Make command reference           |
| `make build`        | Configure and build without running tests |
| `make test`         | Build and run the test suite              |
| `make format`       | Format tracked C++ and header files       |
| `make format-check` | Check formatting without changing files   |
| `make clean`        | Remove generated build artifacts          |
