# The Makefile Tutorial
Here we will be following the tutorial from https://makefiletutorial.com/ made by <a href="https://github.com/theicfire">Chase Lambert</a>. The examples here are in a logical order. Each one is in a separate folder containing one makefile.

<h2 id="prerequisites">Prerequisites</h2>

- Basic knowledge of <a href="https://www.javatpoint.com/compilation-process-in-c">the compilation process in C</a>
- Basic knowledge of <a href="https://www.javatpoint.com/bash">bash scripting</a>
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

<h2 id="contents">Table of Contents</h2>

- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX001%20-%20Hello%20World" id="EX001">EX001 - Hello World</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX002%20-%20Makefile%20Syntax" id="EX002">EX002 - Makefile Syntax</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX003%20-%20Makefile%20Sequence%20of%20Events" id="EX003">EX003 - Makefile Sequence of Events</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX004%20-%20Make%20Clean" id="EX004">EX004 - Make clean</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX005%20-%20Variables" id="EX005">EX005 - Variables</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX006%20-%20Automatic%20Variables" id="EX006">EX006 - Automatic Variables</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX007%20-%20Targets" id="EX007">EX007 - Targets</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX008%20-%20The%20Asterisk%20Wildcard" id="EX008">EX008 - The Asterisk Wildcard</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX009%20-%20The%20Percent%20Sign%20Wildcard" id="EX009">EX009 - The Percent Sign Wildcard</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX010%20-%20Implicit%20Rules" id="EX010">EX010 - Implicit Rules</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX011%20-%20Static%20Pattern%20Rules" id="EX011">EX011 - Static Pattern Rules</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX012%20-%20Pattern%20Rules" id="EX012">EX012 - Pattern Rules</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX013%20-%20Double-Colon%20Rules" id="EX013">EX013 - Double-Colon Rules</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX014%20-%20Command%20Silencing" id="EX014">EX014 - Command Silencing</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX015%20-%20Command%20Execution" id="EX015">EX015 - Command Execution</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX016%20-%20Default%20Shell" id="EX016">EX016 - Default Shell</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX017%20-%20Double%20Dollar%20Sign" id="EX017">EX017 - Double Dollar Sign</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX018%20-%20Error%20Handling" id="EX018">EX018 - Error Handling</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX019%20-%20Recursion" id="EX019">EX019 - Recursion</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX020%20-%20Environment%20Variables" id="EX020">EX020 - Environment Variables</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX021%20-%20Override%20CLI%20Arguments" id="EX021">EX021 - Override CLI Arguments</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX022%20-%20Functions" id="EX022">EX022 - Functions</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX023%20-%20Conditional%20Statement" id="EX023">EX023 - Conditional Statements</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX024%20-%20vpath" id="EX024">EX024 - vpath</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX025%20-%20.PHONY" id="EX025">EX025 - .PHONY</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX026%20-%20.DELETE_ON_ERROR" id="EX026">EX026 - .DELETE_ON_ERROR</a>
- <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/Makefile%20Cookbook" id="cookbook">Makefile Cookbook</a>

<h2 id="resources">Other Resources</h2>

- <a href="https://www.gnu.org/software/make/manual/html_node/index.html">GNU Make Manual</a>
