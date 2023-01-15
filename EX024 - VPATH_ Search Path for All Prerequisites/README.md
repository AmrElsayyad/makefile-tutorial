### VPATH: Search Path for All Prerequisites

The value of the `make` variable `VPATH` specifies a list of directories that `make` should search. Most often, the directories are expected to contain prerequisite files that are not in the current directory; however, `make` uses `VPATH` as a search list for both prerequisites and targets of rules.

Thus, if a file that is listed as a target or prerequisite does not exist in the current directory, `make` searches the directories listed in `VPATH` for a file with that name. If a file is found in one of them, that file may become the prerequisite (see below). Rules may then specify the names of files in the prerequisite list as if they all existed in the current directory.

In the `VPATH` variable, directory names are separated by colons or blanks. The order in which directories are listed is the order followed by `make` in its search. (On MS-DOS and MS-Windows, semi-colons are used as separators of directory names in `VPATH`, since the colon can be used in the pathname itself, after the drive letter.)

For example,

```make
VPATH = src:headers
```

specifies a path containing two directories, `src` and `headers`, which `make` searches in that order.

With this value of `VPATH`, the following rule,

```make
foo.o : foo.c
```

is interpreted as if it were written like this:

```make
foo.o : src/foo.c
```
assuming the file `foo.c` does not exist in the current directory but is found in the directory `src`.

### The vpath Directive

Similar to the `VPATH` variable, but more selective, is the `vpath` directive (note lower case), which allows you to specify a search path for a particular class of file names: those that match a particular pattern. Thus you can supply certain search directories for one class of file names and other directories (or none) for other file names.

There are three forms of the vpath directive:

- _vpath pattern directories_

  Specify the search path directories for file names that match pattern.

  The search path, directories, is a list of directories to be searched, separated by colons (semi-colons on MS-DOS and MS-Windows) or blanks, just like the search path used in the `VPATH` variable.

- _vpath pattern_

  Clear out the search path associated with pattern.

- _vpath_

  Clear all search paths previously specified with vpath directives.

A `vpath` pattern is a string containing a `%` character. The string must match the file name of a prerequisite that is being searched for, the `%` character matching any sequence of zero or more characters (as in pattern rules; see Defining and Redefining Pattern Rules). For example, %.h matches files that end in .h. (If there is no `%`, the pattern must match the prerequisite exactly, which is not useful very often.)

`%` characters in a `vpath` directive’s pattern can be quoted with preceding backslashes (`\`). Backslashes that would otherwise quote `%` characters can be quoted with more backslashes. Backslashes that quote `%` characters or other backslashes are removed from the pattern before it is compared to file names. Backslashes that are not in danger of quoting `%` characters go unmolested.

When a prerequisite fails to exist in the current directory, if the pattern in a `vpath` directive matches the name of the prerequisite file, then the directories in that directive are searched just like (and before) the directories in the `VPATH` variable.

For example,

```make
vpath %.h ../headers
```

tells `make` to look for any prerequisite whose name ends in .h in the directory `../headers` if the file is not found in the current directory.

If several `vpath` patterns match the prerequisite file’s name, then `make` processes each matching `vpath` directive one by one, searching all the directories mentioned in each directive. `make` handles multiple `vpath` directives in the order in which they appear in the makefile; multiple directives with the same pattern are independent of each other.

Thus,

```make
vpath %.c foo
vpath %   blish
vpath %.c bar
```

will look for a file ending in .c in `foo`, then `blish`, then `bar`, while

```make
vpath %.c foo:bar
vpath %   blish
```

will look for a file ending in .c in `foo`, then `bar`, then `blish`.

### Summary

You can use `vpath` to specify where some set of prerequisites exist. The format is: 

`vpath <pattern> <directories, space/colon separated>`

```make
vpath %.h headers
vpath %.c src

some_binary: headers blah.h src blah.c
	touch some_binary

headers:
	mkdir headers

blah.h:
	touch headers/blah.h

src:
	mkdir src

blah.c:
	touch src/blah.c

clean:
	rm -rf headers
	rm -rf src
	rm -f some_binary
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX025%20-%20Phony%20Targets" id="EX025">
		<img src="https://img.shields.io/badge/Next-EX025: Phony Targets-blue.svg">
	</a>
</p>
