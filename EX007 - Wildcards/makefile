# 
# * Wildcard
# 
# * searches your filesystem for matching filenames. 
# 
# I suggest that you always wrap it in the wildcard function,
# because otherwise you may fall into a common pitfall described in the next example.
# 
# * may be used in the target, prerequisites, or in the wildcard function.
#

# Danger: * may not be directly used in a variable definitions
# Danger: When * matches no files, it is left as it is (unless run in the wildcard function)

thing_wrong := *.o	# Don't do this! '*' will not get expanded
thing_right := $(wildcard *.o)

all: three four print one two
	echo all

# Print out file information about every .c file

print: $(wildcard *.c)
	echo print
	ls -la  $?
	echo
	echo 'Note that because there are no .c files, the wildcard here expanded for nothing.' 
	echo

# Fails, because $(thing_wrong) is the string "*.o"

one: $(thing_wrong)
	echo one

# Stays as *.o if there are no files that match this pattern :(
# Same as one.

two: *.o
	echo two

# Works as you would expect! In this case, it does nothing.

three: $(thing_right)
	echo three

# Same as rule three

four: $(wildcard *.o)
	echo four

