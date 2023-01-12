### The all target
Making multiple targets and you want all of them to run? Make an all target. Since this is the first rule listed, it will run by default if `make` is called without specifying a target.

```make
all: one two three

one:
	touch one
two:
	touch two
three:
	touch three
```

### Multiple targets
When there are multiple targets for a rule, the commands will be run for each target.

```make
f1.o f2.o:
	echo $@
# Equivalent to:
# f1.o:
#	 echo f1.o
# f2.o:
#	 echo f2.o
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX008%20-%20The%20Asterisk%20Wildcard" id="EX008">
		Next: EX008 - The Asterisk Wildcard
	</a>
</p>
