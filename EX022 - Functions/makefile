# Functions are mainly just for text processing. Call functions with $(fn, arguments) or ${fn, arguments}. You can make your own using the call builtin function. Make has a decent amount of builtin functions.

CC := gcc

all: substitution space_replace function_syntax pattern_substitution \
	foreach_fun if_fun call_fun shell_fun filter_fun

	echo 'all is done!'

# String Substitution

superman := $(subst not, totally, "I am not superman")

substitution:
	echo
	echo '>>> substitution >>>'
	echo

	echo ${superman}

	echo
	echo '<<< substitution <<<'
	echo

# If you want to replace spaces or commas, use variables

comma := ,
empty:=
space := ${empty} ${empty}
abc := a b c
new_abc := $(subst ${space},${comma},${abc})

space_replace:
	echo
	echo '>>> space_replace >>>'
	echo

	echo ${new_abc}

	echo
	echo '<<< space_replace <<<'
	echo

# Do NOT include spaces in the arguments after the first. That will be seen as part of the string.

more_spaces := $(subst ${space}, ${comma} , ${abc})

function_syntax:
	echo
	echo '>>> function_syntax >>>'
	echo

	echo ${more_spaces}

	echo
	echo '<<< function_syntax <<<'
	echo

# Pattern Substitution

files := a.o b.o l.a c.o
pat_subst := $(patsubst %.o,%.c,${files})

# This is a shorthand for the above

shorthand := ${files:%.o=%.c}

# This is the suffix-only shorthand, and is also equivalent to the above.

suffix := ${files:.o=.c}

pattern_substitution:
	echo
	echo '>>> pattern_substitution >>>'
	echo

	echo ${pat_subst}
	echo ${shorthand}
	echo ${suffix}

	echo
	echo '<<< pattern_substitution <<<'
	echo

# The foreach function

list := who are you

# For each "word" in foo, output that same word with an exclamation after

with_exclamation := $(foreach wrd,$(list),$(wrd)!)

foreach_fun:
	echo
	echo '>>> foreach_fun >>>'
	echo

	echo ${with_exclamation}

	echo
	echo '<<< foreach_fun <<<'
	echo

# The if function

isnt_empty := $(if this-is-not-empty,then!,else!)
empty :=
is_empty := $(if ${empty},then!,else!)

if_fun:
	echo
	echo '>>> if_fun >>>'
	echo

	echo ${isnt_empty}
	echo ${is_empty}

	echo
	echo '<<< if_fun <<<'
	echo

# The call function

sweet_new_fn = Variable Name: $(0) First: $(1) Second: $(2) Empty Variable: $(3)

call_fun:
	echo
	echo '>>> call_fun >>>'
	echo

	echo $(call sweet_new_fn, go, tigers)

	echo
	echo '<<< call_fun <<<'
	echo

# The shell function

shell_fun:
	echo
	echo '>>> shell_fun >>>'
	echo

	echo $(shell ls -la) # Very ugly because the newlines are gone!

	echo
	echo '<<< shell_fun <<<'
	echo

# The filter function

obj_files = foo.result bar.o lose.o main.o
src_files = foo.raw bar.c lose.c

filter_fun: $(obj_files)
	echo
	echo '>>> filter_fun <<<'
	echo

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
