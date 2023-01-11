### Recursive use of make
To recursively call a makefile, use the special `$(MAKE)` instead of make because it will pass the make flags for you and won't itself be affected by them.

```make
new_contents = "hello:\n\ttouch inside_file"

all:
	mkdir -p subdir
	printf ${new_contents} > subdir/makefile
	cd subdir && ${MAKE}

clean:
	rm -rf subdir
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX020%20-%20Environment%20Variables" id="EX020">
		Next: EX020 - Environment Variables
	</a>
</p>
