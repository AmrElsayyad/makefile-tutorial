This _makefile_ ultimately runs all three targets. When you run `make` in the terminal, it will build a program called `blah.exe` in a series of steps:

- `make` selects the target `blah.exe`, because the first target is the default target
- blah requires `blah.o`, so `make` searches for the `blah.o` target
- `blah.o` requires `blah.c`, so `make` searches for the `blah.c` target
- `blah.c` has no dependencies, so the echo command is run
- The rule for target `blah.o` is then run, because all of the `blah.o` dependencies are finished
- Finally, the rule for target `blah.exe` is run, because all the `blah.exe` dependencies are finished
- That's it: `blah.exe` is a compiled c program

```make
# blah requires blah.o, so make searches for the blah.o target
blah.exe: blah.o
	gcc blah.o -o blah.exe				# Runs third

# blah.o requires blah.c, so make searches for the blah.c target
blah.o: blah.c
	gcc -c blah.c -o blah.o				# Runs second

# blah.c has no dependencies, so the echo command is run
blah.c:
	echo "int main() { return 0; }" > blah.c	# Runs first
```

If you delete `blah.c`, all three targets will be rerun. If you edit it (and thus change the timestamp to newer than `blah.o`), the first two targets will run. If you run touch `blah.o` (and thus change the timestamp to newer than `blah.exe`), then only the first target will run. If you change nothing, none of the targets will run. Try it out!

<div align="right">
  <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX004%20-%20Make%20clean">
  	<img src="https://img.shields.io/badge/Next-EX004: Make clean-blue.svg">
  </a>
</div>
