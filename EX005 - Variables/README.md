### Basics of Variable References

Variables in `make` can only be **strings**. Reference variables using either `${}` or `$()`.

Here's an example of using variables:

```make
files := file1 file2

some_file: ${files}
	echo "Look at this variable: " ${files}
	touch some_file

file1:
	touch file1

file2:
	touch file2
```


### Quotes

Single or double quotes have no meaning to Make. They are simply characters that are assigned to the variable. Quotes are useful to shell/bash, though, and you need them in commands like `printf`.

```make
quoted	:= '\nOne Two\n'	# Not recommended. 'quoted' is assigned to the string "'\nOne Two\n'	"
not_quoted := \nOne Two\n	# 'not_quoted' is assigned to the string "\nOne Two\n	"

quotes:
	printf ${quoted}
	printf '${quoted}'
	printf ${not_quoted}
	printf '${not_quoted}'
```

### Trailing whitespace

Spaces at the end of a line are not stripped, but those at the start are. To make a variable with a single space, use `${nullstring}`.

```make
with_spaces = hello   # with_spaces has many spaces after "hello"
after = ${with_spaces}there

nullstring =
space = ${nullstring} # Make a variable with a single space.

whitespaces: 
	echo "${after}"
	echo start"${space}"end
```

An undefined variable is actually an empty string!

```make
empty:
	# Undefined variables are just empty strings!
	echo ${nowhere}
```

### Variable Assignment

You can define variables using two methods:

- recursive (use `=`) - only looks for the variables when the command is used, not when it's defined.
- simply-expanded (use `:=`) - like normal imperative programming -- only those defined so far get expanded.

Here's an example on the difference between recursive and simply-expanded variables:

```make
# Recursive variable. This will print "later" below
recursive = blah ${later_variable}

# Simply-expanded variable. This will not print "later" below
simple := blah ${later_variable}

later_variable = later

recursive_vs_simple:
	echo ${recursive}
	echo ${simple}
```

Simply-expanded variables (using `:=`) allows you to append to itself. Recursive definitions will give an infinite loop error.

```make
var = hello
# var gets defined as a simply-expanded variable (`:=`)
# Thus can handle appending
var := ${var} there

concat: 
	echo ${var}
```

You can use `+=` to append to variables:

```make
str := start
str += more

append: 
	echo ${str}
```

### Conditional Variable Assignment

There is another assignment operator for variables, `?=`. This is called a conditional variable assignment operator, because it only has an effect if the variable is not yet defined.

```make
set = hello
set ?= will not be set
unset ?= will be set

set_if_unset: 
	echo ${set}
	echo ${unset}
```

> Note: If you want `make` to run silently, use the `-s` option.


<p align="right">
  <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX006%20-%20Automatic%20Variables">
  	<img src="https://img.shields.io/badge/Next-EX006: Automatic Variables-blue.svg">
  </a>
</p>
