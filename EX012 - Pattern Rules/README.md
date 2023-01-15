Pattern rules are often used but quite confusing. You can look at them as two ways:
- A way to define your own implicit rules
- A simpler form of static pattern rules

Let's start with an example first:

```make
CC := gcc

objects = foo.o bar.o all.o
all: $(objects)

# Define a pattern rule that compiles every .c file into a .o file
%.o : %.c
		$(CC) -c $(CFLAGS) $(CPPFLAGS) $< -o $@

all.c:
	echo 'int main() { return 0; }' > $@
```

Pattern rules contain a `%` in the target. This `%` matches any nonempty string, and the other characters match themselves. `%` in a prerequisite of a pattern rule stands for the same stem that was matched by the `%` in the target.

Here's another example:

```make
# Define a pattern rule that has no pattern in the prerequisites.
# This just creates a return 0 .c files when needed.
%.c:
	touch $@
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX013%20-%20Double-Colon%20Rules" id="EX013">
		<img src="https://img.shields.io/badge/Next-EX013: Double-Colon Rules-blue.svg">
	</a>
</p>
