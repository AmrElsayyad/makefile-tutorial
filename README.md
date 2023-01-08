# The Makefile Tutorial
Here we will be following the tutorial from https://makefiletutorial.com/ made by <a href="https://github.com/theicfire">Chase Lambert</a>. The examples here are in a logical order. Each one is in a separate folder containing only one makefile.

<h2 id="prerequisites">Prerequisites</h2>

- <a href="https://www.javatpoint.com/compilation-process-in-c">Compilation Process in C</a>
- <a href="https://www.javatpoint.com/bash">BASH Scripting</a>
- `gcc` and `make` installed
- <a href="https://git-scm.com/downloads">Git Bash</a> installed, if using windows.

<h2 id="why-do-makefiles-exist">Why do Makefiles exist?</h2>
<p>Makefiles are used to help decide which parts of a large program need to be recompiled. In the vast majority of cases, C or C++ files are compiled. Other languages typically have their own tools that serve a similar purpose as Make. Make can also be used beyond compilation too, when you need a series of instructions to run depending on what files have changed. This tutorial will focus on the C/C++ compilation use case.</p>
<p>Here's an example dependency graph that you might build with Make. If any file's dependencies changes, then the file will get recompiled:</p>
<div class="center">
<img src="https://makefiletutorial.com/assets/dependency_graph.png">
</div>

<h2 id="what-alternatives-are-there-to-make">What alternatives are there to Make?</h2>
<p>Popular C/C++ alternative build systems are <a href="https://scons.org/">SCons</a>, <a href="https://cmake.org/">CMake</a>, <a href="https://bazel.build/">Bazel</a>, and <a href="https://ninja-build.org/">Ninja</a>. Some code editors like <a href="https://visualstudio.microsoft.com/">Microsoft Visual Studio</a> have their own built in build tools. For Java, there's <a href="https://ant.apache.org/">Ant</a>, <a href="https://maven.apache.org/what-is-maven.html">Maven</a>, and <a href="https://gradle.org/">Gradle</a>. Other languages like Go and Rust have their own build tools.</p>
<p>Interpreted languages like Python, Ruby, and Javascript don't require an analogue to Makefiles. The goal of Makefiles is to compile whatever files need to be compiled, based on what files have changed. But when files in interpreted languages change, nothing needs to get recompiled. When the program runs, the most recent version of the file is used.</p>
<h2 id="the-versions-and-types-of-make">The versions and types of Make</h2>
<p>There are a variety of implementations of Make, but most of this guide will work on whatever version you're using. However, it's specifically written for GNU Make, which is the standard implementation on Linux and MacOS. All the examples work for Make versions 3 and 4, which are nearly equivalent other than some esoteric differences.</p>

<h2 id="Resources">Other Resources</h2>

- <a href="https://www.gnu.org/software/make/manual/html_node/index.html">GNU Make Manual</a>
