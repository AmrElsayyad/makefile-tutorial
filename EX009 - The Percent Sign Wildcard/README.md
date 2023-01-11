### % Wildcard
% is really useful, but is somewhat confusing because of the variety of situations it can be used in:
- When used in "matching" mode, it matches one or more characters in a string. This match is called the stem.
- When used in "replacing" mode, it takes the stem that was matched and replaces that in a string.
- % is most often used in rule definitions and in some specific functions.

```make
objects = foo.o bar.o all.o

all: ${objects}
	gcc $^ -o $@

%.o: %.c
	gcc -c $^ -o $@

all.c:
	echo "int main() { return 0; }" > all.c

%.c:
	touch $@

clean:
	rm -f *.c *.o all
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX010%20-%20Implicit%20Rules" id="EX010">
		Next: EX010 - Implicit Rules
	</a>
</p>
