# When Make starts, it automatically creates Make variables out of all the environment variables that are set when it's executed.

all: one two three four
	echo 'all is done!'

# Run this with "export var1='I am an environment variable'; make one"
one:
	echo
	echo '>>> one >>>'
	echo

	# Print out the Shell variable
	echo $$var1

	# Print out the Make variable
	echo ${var1}

	echo
	echo '<<< one <<<'
	echo

# The export directive takes a variable and sets it the environment for all shell commands in all the recipes:

var2=var2: created inside of Make
export var2

two:
	echo
	echo '>>> two >>>'
	echo

	echo ${var2}
	echo $$var2

	echo
	echo '<<< two <<<'
	echo

# As such, when you run the make command inside of make, you can use the export directive to make it accessible to sub-make commands.
# In this example, 'var4' is exported such that the makefile in subdir can use it.

var3 = "hello:\n\techo \$${var4}\n"

three:
	echo
	echo '>>> three >>>'
	echo

	mkdir -p subdir
	printf ${var3} > subdir/makefile
	@echo "---MAKEFILE CONTENTS---"
	@cd subdir && cat makefile
	@echo "---END MAKEFILE CONTENTS---"
	cd subdir && ${MAKE}

	echo
	echo '<<< three <<<'
	echo

# Note that variables and exports. They are set/affected globally.

var4 = "The subdirectory can see me!"
export var4

# This would nullify the line above: unexport var4


# You need to export variables to have them run in the shell as well.

local=this will only work locally
export global=we can run subcommands with this

four:
	echo
	echo '>>> four >>>'
	echo

	echo ${local}
	echo $$local
	echo ${global}
	echo $$global

	echo
	echo '<<< four <<<'
	echo

clean:
	rm -rf subdir
