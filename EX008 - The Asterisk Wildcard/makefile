thing_wrong := *.o	# Don't do this! '*' will not get expanded
thing_right := $(wildcard *.o)

all: print one two three four

# Print out file information about every .c file

print: $(wildcard *.c)
	ls -la $?

# Works as you would expect! In this case, it does nothing.

one: $(thing_right)

# Same as rule three

two: $(wildcard *.o)

# Fails, because $(thing_wrong) is the string "*.o"

three: $(thing_wrong)

# Stays as *.o if there are no files that match this pattern :(
# Same as three.

four: *.o
