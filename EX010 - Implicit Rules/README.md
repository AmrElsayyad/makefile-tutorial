Make loves c compilation. And every time it expresses its love, things get confusing. Perhaps the most confusing part of Make is the magic/automatic rules that are made. Make calls these "implicit" rules. I don't personally agree with this design decision, and I don't recommend using them, but they're often used and are thus useful to know.

Here's a list of implicit rules:
- Compiling a C program: n.o is made automatically from n.c with a command of the form:

  `$(CC) -c $(CPPFLAGS) $(CFLAGS) $^ -o $@`

- Compiling a C++ program: n.o is made automatically from n.cc or n.cpp with a command of the form:

  `$(CXX) -c $(CPPFLAGS) $(CXXFLAGS) $^ -o $@`

- Linking a single object file: n is made automatically from n.o by running the command:

  `$(CC) $(LDFLAGS) $^ $(LOADLIBES) $(LDLIBS) -o $@`

The important variables used by implicit rules are:
- `CC`: Program for compiling C programs; default cc
- `CXX`: Program for compiling C++ programs; default g++
- `CFLAGS`: Extra flags to give to the C compiler
- `CXXFLAGS`: Extra flags to give to the C++ compiler
- `CPPFLAGS`: Extra flags to give to the C preprocessor
- `LDFLAGS`: Extra flags to give to compilers when they are supposed to invoke the linker

Let's see how we can now build a C program without ever explicitly telling Make how to do the compililation:

```make
CC = gcc # Flag for implicit rules
CFLAGS = -g # Flag for implicit rules. Turn on debug info

# Implicit rule #1: blah is built via the C linker implicit rule
# Implicit rule #2: blah.o is built via the C compilation implicit rule, because blah.c exists
blah: blah.o

blah.c:
	echo "int main() { return 0; }" > blah.c

clean:
	rm -f blah*
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX011%20-%20Static%20Pattern%20Rules" id="EX011">
		Next: EX011 - Static Pattern Rules
	</a>
</p>
