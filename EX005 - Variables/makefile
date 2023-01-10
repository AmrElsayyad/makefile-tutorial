files := file1 file2
a := \nOne Two\n	# a is assigned to the string "one two"
b := '\nOne Two\n'	# Not recommended. b is assigned to the string "'one two'"

all: print some_file rule1 rule2 rule3 rule4 rule5 rule6 rule7 other

print:
	printf ${a}
	printf '${a}'
	printf ${b}
	printf '${b}'

some_file: ${files}
	echo "Look at this variable: " ${files}
	touch some_file

file1:
	touch file1

file2:
	touch file2

# Recursive variable. This will print "later" below
one = one ${later_variable}

# Simply expanded variable. This will not print "later" below
two := two ${later_variable}

later_variable = later

rule1: 
	echo ${one}
	echo ${two}

# Simply expanded {using :=} allows you to append to a variable. Recursive definitions will give an infinite loop error.

three = hello
# one gets defined as a simply expanded variable {:=} and thus can handle appending
three := ${three} there

rule2: 
	echo ${three}

# ?= only sets variables if they have not yet been set

four = hello
four ?= will not be set
five ?= will be set

rule3: 
	echo ${four}
	echo ${five}

# Spaces at the end of a line are not stripped, but those at the start are. To make a variable with a single space, use ${nullstring}

with_spaces = hello   # with_spaces has many spaces after "hello"
after = ${with_spaces}there

nullstring =
space = ${nullstring} # Make a variable with a single space.

rule4: 
	echo "${after}"
	echo start"${space}"end

# An undefined variable is actually an empty string!

rule5: 
	# Undefined variables are just empty strings!
	echo ${nowhere}

# Use += to append

foo := start
foo += more

rule6: 
	echo ${foo}

# Target-specific variables
# Variables can be assigned for specific targets

rule7: cool = cool

rule7:
	echo cool is defined: ${cool}

other:
	echo cool is nothing: ${cool}

clean:
	rm -f file1 file2 some_file

