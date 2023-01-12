# Run this with `make -s` if you don't want to print the commands.

all: some_file quotes whitespaces empty recursive_vs_simple concat append set_if_unset
	echo 'all is done!'


# some_file

files := file1 file2

some_file: ${files}
	echo
	echo '>>> some_file >>>'
	echo

	echo "Look at this variable: " ${files}
	touch some_file

	echo
	echo '<<< some_file <<<'
	echo

file1:
	touch file1

file2:
	touch file2


# Quotes

quoted	:= '\nOne Two\n'	# Not recommended. 'quoted' is assigned to the string "'\nOne Two\n'	"
not_quoted := \nOne Two\n	# 'not_quoted' is assigned to the string "\nOne Two\n	"

quotes:
	echo
	echo '>>> quotes >>>'
	echo

	printf ${quoted}
	printf '${quoted}'
	printf ${not_quoted}
	printf '${not_quoted}'

	echo
	echo '<<< quotes <<<'
	echo


# Whitespaces

with_spaces = hello   # with_spaces has many spaces after "hello"
after = ${with_spaces}there

nullstring =
space = ${nullstring} # Make a variable with a single space.

whitespaces:
	echo
	echo '>>> whitespaces >>>'
	echo

	echo "${after}"
	echo start"${space}"end

	echo
	echo '<<< whitespaces <<<'
	echo


# An undefined variable is actually an empty string!

empty:
	echo
	echo '>>> empty >>>'
	echo

	# Undefined variables are just empty strings!
	echo ${nowhere}

	echo
	echo '<<< empty <<<'
	echo


# Recursive and simply-expanded variables

# Recursive variable. This will print "later" below
recursive = blah ${later_variable}

# Simply-expanded variable. This will not print "later" below
simple := blah ${later_variable}

later_variable = later

recursive_vs_simple:
	echo
	echo '>>> recursive_vs_simple >>>'
	echo

	echo ${recursive}
	echo ${simple}

	echo
	echo '<<< recursive_vs_simple <<<'
	echo


# Simply-expanded variables (using `:=`) allows you to append to itself. 
# Recursive definitions will give an infinite loop error.

var = hello
# var gets defined as a simply-expanded variable (`:=`)
# Thus can handle appending
var := ${var} there

concat:
	echo
	echo '>>> concat >>>'
	echo

	echo ${var}

	echo
	echo '<<< concat <<<'
	echo


# Use `+=` to append

str := start
str += more

append:
	echo
	echo '>>> append >>>'
	echo

	echo ${str}

	echo
	echo '<<< append <<<'
	echo


# `?=` only sets variables if they have not yet been set

set = hello
set ?= will not be set
unset ?= will be set

set_if_unset:
	echo
	echo '>>> set_if_unset >>>'
	echo

	echo ${set}
	echo ${unset}

	echo
	echo '<<< set_if_unset <<<'
	echo


clean:
	rm -f file1 file2 some_file
