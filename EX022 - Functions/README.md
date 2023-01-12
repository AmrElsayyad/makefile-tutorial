Functions are mainly just for text processing. Call functions with `$(fn, arguments)` or `${fn, arguments}`. You can make your own using the call builtin function. Make has a decent amount of [builtin functions](https://www.gnu.org/software/make/manual/html_node/Functions.html).

### The substitute function

`subst` performs a textual replacement on the text text: each occurrence of from is replaced by to. The result is substituted for the function call. For example:

```make
superman := $(subst not, totally, "I am not superman")

substitution:
	echo ${superman}
```

If you want to replace spaces or commas, use variables:

```make
comma := ,
empty:=
space := ${empty} ${empty}
abc := a b c
new_abc := $(subst ${space},${comma},${abc})

space_replace: 
	echo ${new_abc}
```

Do NOT include spaces in the arguments after the first. That will be seen as part of the string.

```make
more_spaces := $(subst ${space}, ${comma} , ${abc})

function_syntax:
	echo ${more_spaces}
```

### Pattern Substitution
`$(patsubst pattern,replacement,text)` does the following:
> "Finds whitespace-separated words in text that match pattern and replaces them with replacement. Here pattern may contain a `%` which acts as a wildcard, matching any number of any characters within a word. If replacement also contains a `%`, the `%` is replaced by the text that matched the `%` in pattern. Only the first `%` in the pattern and replacement is treated this way; any subsequent `%` is unchanged." -- GNU docs

The substitution reference `$(text:pattern=replacement)` is a shorthand for this.

There's another shorthand that that replaces only suffixes: `$(text:suffix=replacement)`. No `%` wildcard is used here.

Note: don't add extra spaces for this shorthand. It will be seen as a search or replacement term.

```make
files := a.o b.o l.a c.o
pat_subst := $(patsubst %.o,%.c,${files})

# This is a shorthand for the above

shorthand := ${files:%.o=%.c}

# This is the suffix-only shorthand, and is also equivalent to the above.

suffix := ${files:.o=.c}

pattern_substitution:
	echo ${pat_subst}
	echo ${shorthand}
	echo ${suffix}
```

### The foreach function
The foreach function looks like this: `$(foreach var,list,text)`. It converts one list of words (separated by spaces) to another. `var` is set to each word in list, and text is expanded for each word.

This appends an exclamation after each word:

```make
list := who are you

# For each "word" in foo, output that same word with an exclamation after

with_exclamation := $(foreach wrd,$(list),$(wrd)!)

foreach_fun:
	echo ${with_exclamation}
```

### The if function
`if` checks if the first argument is nonempty. If so runs the second argument, otherwise runs the third.

```make
isnt_empty := $(if this-is-not-empty,then!,else!)
empty :=
is_empty := $(if ${empty},then!,else!)

if_fun:
	echo ${isnt_empty}
	echo ${is_empty}
```

### The call function
Make supports creating basic functions. You "define" the function just by creating a variable, but use the parameters `$(0)`, `$(1)`, etc. You then call the function with the special `call` function. The syntax is `$(call variable,param,param)`. `$(0)` is the variable, while `$(1)`, `$(2)`, etc. are the params.

```make
sweet_new_fn = Variable Name: $(0) First: $(1) Second: $(2) Empty Variable: $(3)

call_fun:
	echo $(call sweet_new_fn, go, tigers)
```

### The shell function
`shell` - This calls the shell, but it replaces newlines with spaces!

More about [the shell function](https://www.gnu.org/software/make/manual/html_node/Shell-Function.html).

```make
shell_fun:
	echo $(shell ls -la) # Very ugly because the newlines are gone!
```

### The filter function
Returns all whitespace-separated words in text that do match any of the pattern words, removing any words that do not match. The patterns are written using `%`, just like the patterns used in the patsubst function above.

The `filter` function can be used to separate out different types of strings (such as file names) in a variable. For example:

```make
obj_files = foo.result bar.o lose.o main.o
src_files = foo.raw bar.c lose.c

filter_fun: $(obj_files)
	echo filter_fun

# Ex 1: .o files depend on .c files. Though we don't actually make the .o file.
$(filter %.o,$(obj_files)): %.o: %.c
	echo "target: $@ prereq: $<"

# Ex 2: .result files depend on .raw files. Though we don't actually make the .result file.
$(filter %.result,$(obj_files)): %.result: %.raw
	echo "target: $@ prereq: $<" 

%.c %.raw:
	touch $@

clean:
	rm -f *.c *.o *.raw
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX023%20-%20Conditional%20Statements" id="EX023">
		Next: EX023 - Conditional Statements
	</a>
</p>
