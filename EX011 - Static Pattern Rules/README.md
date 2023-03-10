Static pattern rules are another way to write less in a Makefile, but I'd say are more useful and a bit less "magic". Here's their syntax:

```make
targets...: target-pattern: prereq-patterns ...
	commands
```

The essence is that the given target is matched by the target-pattern (via a `%` wildcard). Whatever was matched is called the stem. The stem is then substituted into the prereq-pattern, to generate the target's prereqs.

```make
CC := gcc

objects = foo.o bar.o all.o

all: $(objects)

# These files compile via implicit rules
# Syntax - targets ...: target-pattern: prereq-patterns ...
# In the case of the first target, foo.o, the target-pattern matches foo.o and sets the "stem" to be "foo".
# It then replaces the '%' in prereq-patterns with that stem

$(objects): %.o: %.c

all.c:
	echo "int main() { return 0; }" > all.c

%.c:
	touch $@

clean:
	rm -f *.c *.o all
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX012%20-%20Pattern%20Rules" id="EX012">
		<img src="https://img.shields.io/badge/Next-EX012: Pattern Rules-blue.svg">
	</a>
</p>
