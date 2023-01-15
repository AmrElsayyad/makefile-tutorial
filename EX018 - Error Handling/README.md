- Add `-k` when running `make` to continue running even in the face of errors.
- Add a `-` before a command to suppress the error.
- Add `-i` to `make` to have this happen for every command.

```make
all: one two
	echo all

one:
	# This error will cause 'make' to fail and stop.
	false

	echo one

two:
	# This error will be printed but ignored, and 'make' will continue to run
	-false

	echo two
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX019%20-%20Recursion" id="EX019">
		<img src="https://img.shields.io/badge/Next-EX019: Recursion-blue.svg">
	</a>
</p>
