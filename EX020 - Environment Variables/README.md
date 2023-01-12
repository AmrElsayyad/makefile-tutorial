When Make starts, it automatically creates Make variables out of all the environment variables that are set when it's executed.

```make
all: one two three four

# Run this with "export var1='I am an environment variable'; make one"
one:
	# Print out the Shell variable
	echo $$var1

	# Print out the Make variable
	echo ${var1}
```

The `export` directive takes a variable and sets it the environment for all shell commands in all the recipes:

```make
var2=var2: created inside of Make
export var2

two:
	echo ${var2}
	echo $$var2
```

As such, when you run the make command inside of make, you can use the `export` directive to make it accessible to sub-make commands. In this example, `var4` is exported such that the makefile in `subdir` can use it.

```make
var3 = "hello:\n\techo \$${var4}\n"

three:
	mkdir -p subdir
	printf ${var3} > subdir/makefile
	@echo "---MAKEFILE CONTENTS---"
	@cd subdir && cat makefile
	@echo "---END MAKEFILE CONTENTS---"
	cd subdir && ${MAKE}

Note that variables and exports. They are set/affected globally.

var4 = "The subdirectory can see me!"
export var4

# This would nullify the line above: unexport var4

clean:
	rm -rf subdir
```

You need to export variables to have them run in the shell as well.

```make
local=this will only work locally
export global=we can run subcommands with this

four:
	echo ${local}
	echo $$local
	echo ${global}
	echo $$global
```

> Note that you can use `.EXPORT_ALL_VARIABLES` exports all variables for you.

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX021%20-%20Override%20CLI%20Arguments" id="EX021">
		Next: EX021 - Override CLI Arguments
	</a>
</p>
