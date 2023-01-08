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

all: print three four one two
	# Note the order of the prerequisites and that make would fail to run rule 'one'
	touch all

# Print out file information about every .c file

print: $(wildcard *.c)
	# '$$(wildcard *.c)' in the prerequisites would expand for nothing, since there are no .c files in the directory.
	# That would lead '$$?' in 'ls -la $$?' to expand for nothing, because '$$?' is an automatic variable that expands for the prerequisites.
	# That would turn the command 'ls -la $$?' into 'ls -la'. 
	ls -la $?
	touch print

# Fails, because $(thing_wrong) is the string "*.o"

one: $(thing_wrong)
	touch one

# Stays as *.o if there are no files that match this pattern :(
# Same as one.

two: *.o
	touch two

# Works as you would expect! In this case, it does nothing.

three: $(thing_right)
	touch three

# Same as rule three

four: $(wildcard *.o)
	touch four

clean:
	rm -f print one two three four all
