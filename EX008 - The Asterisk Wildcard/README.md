### `*` Wildcard
`*` searches your filesystem for matching filenames. `*` may be used in the target, prerequisites, or in the wildcard function. In the example below, `$(wildcard *.c)` in the prerequisites would expand for nothing, since there are no .c files in the directory. That would lead `$?` in `ls -la $?` to expand for nothing, because `$?` is an automatic variable that expands for the prerequisites. That would turn the command `ls -la $?` into `ls -la`.

```make
# Print out file information about every .c file

print: $(wildcard *.c)
	ls -la $?
	touch print
```

I suggest that you always wrap it in the wildcard function, because otherwise you may fall into a common pitfall described in the next example. `*` may not be directly used in a variable definitions. When `*` matches no files, it is left as it is (unless run in the wildcard function).

```make
thing_wrong := *.o	# Don't do this! '*' will not get expanded
thing_right := $(wildcard *.o)

all: one two three four

# Works as you would expect! In this case, it does nothing.

one: $(thing_right)

# Same as rule three

two: $(wildcard *.o)

# Fails, because $(thing_wrong) is the string "*.o"

three: $(thing_wrong)

# Stays as *.o if there are no files that match this pattern :(
# Same as three.

four: *.o
```

This would output:

```Shell
make: *** No rule to make target '*.o', needed by 'three'.  Stop.
```

Note that `*.o` did not expand and was taken literally.

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX009%20-%20The%20Percent%20Sign%20Wildcard" id="EX009">
		Next: EX009 - The Percent Sign Wildcard
	</a>
</p>
