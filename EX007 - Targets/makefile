# The all target
# Making multiple targets and you want all of them to run? Make an all target.
# Since this is the first rule listed, it will run by default if make is called without specifying a target.

all: one two three f1.o f2.o

one:
	touch one
two:
	touch two
three:
	touch three

# Multiple targets
# When there are multiple targets for a rule, the commands will be run for each target.
# $@ is an automatic variable that contains the target name.

f1.o f2.o:
	echo $@
# Equivalent to:
# f1.o:
#	 echo f1.o
# f2.o:
#	 echo f2.o

clean:
	rm -f one two three

