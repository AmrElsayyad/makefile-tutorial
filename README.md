# Makefile Tutorial

This tutorial provides a step-by-step guide that covers the basics of _makefiles_. The tutorial was built on https://makefiletutorial.com created by [Chase Lambert](https://github.com/theicfire). I added more information from the [GNU Make Manual](https://www.gnu.org/software/make/manual/html_node/index.html) to add some clarifications. The examples are available in separate folders. Each folder has its own _makefile_ containing code that is discussed in a _README_ file. The tutorial examples are progressive so that each step is built on the previous step. At the end you'll be seeing how various topics all work together in an example project (see [Makefile Cookbook](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/Makefile%20Cookbook)).

## Prerequisites

- Basic knowledge of [the compilation process in C](https://www.javatpoint.com/compilation-process-in-c)
- Basic knowledge of [bash scripting](https://www.javatpoint.com/bash)
- `gcc` and `make` installed
- [Git Bash](https://git-scm.com/downloads) installed, if using windows.

## Why do makefiles exist?

Makefiles are used to help decide which parts of a large program need to be recompiled. In the vast majority of cases, C or C++ files are compiled. Other languages typically have their own tools that serve a similar purpose as `make`. `make` can also be used beyond compilation too, when you need a series of instructions to run depending on what files have changed. This tutorial will focus on the C/C++ compilation use case.

Here's an example dependency graph that you might build with `make`. If any file's dependencies changes, then the file will get recompiled:

<div class="center">
<img src="https://makefiletutorial.com/assets/dependency_graph.png">
</div>

## What alternatives are there to Make?

Popular C/C++ alternative build systems are [SCons](https://scons.org/), [CMake](https://cmake.org/), [Bazel](https://bazel.build/), and [Ninja](https://ninja-build.org/). Some code editors like [Microsoft Visual Studio](https://visualstudio.microsoft.com/) have their own built in build tools. For Java, there's [Ant](https://ant.apache.org/), [Maven](https://maven.apache.org/what-is-maven.html), and [Gradle](https://gradle.org/). Other languages like Go and Rust have their own build tools.

Interpreted languages like Python, Ruby, and Javascript don't require an analogue to makefiles. The goal of makefiles is to compile whatever files need to be compiled, based on what files have changed. But when files in interpreted languages change, nothing needs to get recompiled. When the program runs, the most recent version of the file is used.

## The versions and types of Make

There are a variety of implementations of _Make_, but most of this guide will work on whatever version you're using. However, it's specifically written for _GNU Make_, which is the standard implementation on _Linux_ and _MacOS_. All the examples work for _Make_ versions 3 and 4, which are nearly equivalent other than some esoteric differences.

## Table of Contents

- [EX001 - Hello World](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX001%20-%20Hello%20World)
- [EX002 - Makefile Syntax](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX002%20-%20Makefile%20Syntax)
- [EX003 - Makefile Sequence of Events](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX003%20-%20Makefile%20Sequence%20of%20Events)
- [EX004 - Make clean](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX004%20-%20Make%20clean)
- [EX005 - Variables](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX005%20-%20Variables)
- [EX006 - Automatic Variables](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX006%20-%20Automatic%20Variables)
- [EX007 - Targets](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX007%20-%20Targets)
- [EX008 - The Asterisk Wildcard](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX008%20-%20The%20Asterisk%20Wildcard)
- [EX009 - The Percent Sign Wildcard](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX009%20-%20The%20Percent%20Sign%20Wildcard)
- [EX010 - Implicit Rules](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX010%20-%20Implicit%20Rules)
- [EX011 - Static Pattern Rules](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX011%20-%20Static%20Pattern%20Rules)
- [EX012 - Pattern Rules](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX012%20-%20Pattern%20Rules)
- [EX013 - Double-Colon Rules](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX013%20-%20Double-Colon%20Rules)
- [EX014 - Command Silencing](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX014%20-%20Command%20Silencing)
- [EX015 - Command Execution](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX015%20-%20Command%20Execution)
- [EX016 - Default Shell](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX016%20-%20Default%20Shell)
- [EX017 - Double Dollar Sign](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX017%20-%20Double%20Dollar%20Sign)
- [EX018 - Error Handling](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX018%20-%20Error%20Handling)
- [EX019 - Recursion](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX019%20-%20Recursion)
- [EX020 - Environment Variables](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX020%20-%20Environment%20Variables)
- [EX021 - Override CLI Arguments](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX021%20-%20Override%20CLI%20Arguments)
- [EX022 - Functions](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX022%20-%20Functions)
- [EX023 - Conditional Statements](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX023%20-%20Conditional%20Statements)
- [EX024 - VPATH\_ Search Path for All Prerequisites](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX024%20-%20VPATH_%20Search%20Path%20for%20All%20Prerequisites)
- [EX025 - Phony Targets](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX025%20-%20Phony%20Targets)
- [Makefile Cookbook](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/Makefile%20Cookbook)

## Resources

- [Makefile Tutorial](https://makefiletutorial.com)
- [GNU Make Manual](https://www.gnu.org/software/make/manual/html_node/index.html)
