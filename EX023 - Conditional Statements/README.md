### Conditional if/else

```make
var1 = ok

rule1:
ifeq (${var1}, ok)
	echo "var1 equals ok"
else
	echo "nope"
endif
```

### Check if a variable is empty

```make
nullstring =
var2 = $(nullstring) # end of line; there is a space here

rule2:
ifeq ($(strip ${var2}),)
	echo "var2 is empty after being stripped"
endif
ifeq (${nullstring},)
	echo "nullstring doesn't even have spaces"
endif
```

### Check if a variable is defined
ifdef does not expand variable references; it just sees if something is defined at all

```make
bar =
foo = ${bar}

rule3:
ifdef foo
	echo "foo is defined"
endif
ifndef bar
	echo "but bar is not"
endif
```

### ${makeflags}
This example shows you how to test make flags with `findstring` and `MAKEFLAGS`.

Run this example with `make -i` to see it print out the echo statement.

```make
rule4:
# Search for the "-i" flag. MAKEFLAGS is just a list of single characters, one per flag. So look for "i" in this case.
ifneq (,$(findstring i, ${MAKEFLAGS}))
	echo "i was passed to MAKEFLAGS"
endif
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX024%20-%20vpath" id="EX024">
		Next: EX024 - vpath
	</a>
</p>