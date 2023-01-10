# First Functions
# Functions are mainly just for text processing. Call functions with $(fn, arguments) or ${fn, arguments}. You can make your own using the call builtin function. Make has a decent amount of builtin functions.

all: rule1 rule2 rule3 rule4 rule5 rule6 rule7 rule8

var1 := $(subst not, totally, "I am not superman")

rule1: 
	echo ${var1}

# If you want to replace spaces or commas, use variables

comma := ,
empty:=
space := ${empty} ${empty}
var2 := a b c
var3 := $(subst ${space},${comma},${var2})

rule2: 
	echo ${var3}

# Do NOT include spaces in the arguments after the first. That will be seen as part of the string.

var4 := $(subst ${space}, ${comma} , ${var2})

rule3:
	echo ${var4}

# String Substitution
# $(patsubst pattern,replacement,text) does the following:
# "Finds whitespace-separated words in text that match pattern and replaces them with replacement.
# Here pattern may contain a ‘%’ which acts as a wildcard, matching any number of any characters within a word.
# If replacement also contains a ‘%’, the ‘%’ is replaced by the text that matched the ‘%’ in pattern.
# Only the first ‘%’ in the pattern and replacement is treated this way; any subsequent ‘%’ is unchanged." (GNU docs)

# The substitution reference $(text:pattern=replacement) is a shorthand for this.

# There's another shorthand that that replaces only suffixes: $(text:suffix=replacement). No % wildcard is used here.

# Note: don't add extra spaces for this shorthand. It will be seen as a search or replacement term.

var4 := a.o b.o l.a c.o
var5 := $(patsubst %.o,%.c,${var4})

# This is a shorthand for the above

var6 := ${var5:%.o=%.c}

# This is the suffix-only shorthand, and is also equivalent to the above.

var7 := ${var5:.o=.c}

rule4:
	echo ${var5}
	echo ${var6}
	echo ${var7}

# The foreach function
# The foreach function looks like this: $(foreach var,list,text).
# It converts one list of words (separated by spaces) to another.
# var is set to each word in list, and text is expanded for each word.

# This appends an exclamation after each word:

var8 := who are you

# For each "word" in foo, output that same word with an exclamation after

var9 := $(foreach wrd,$(var8),$(wrd)!)

rule5:
	echo ${var9}

# The if function
# if checks if the first argument is nonempty. 
# If so runs the second argument, otherwise runs the third.

var10 := $(if this-is-not-empty,then!,else!)
empty :=
var11 := $(if ${empty},then!,else!)

rule6:
	echo ${var10}
	echo ${var11}

# The call function
# Make supports creating basic functions.
# You "define" the function just by creating a variable, but use the parameters $(0), $(1), etc.
# You then call the function with the special call function.
# The syntax is $(call variable,param,param).
# $(0) is the variable, while $(1), $(2), etc. are the params.

sweet_new_fn = Variable Name: $(0) First: $(1) Second: $(2) Empty Variable: $(3)

rule7:
	echo $(call sweet_new_fn, go, tigers)

# The shell function
# shell - This calls the shell, but it replaces newlines with spaces!

rule8: 
	echo $(shell ls -la) # Very ugly because the newlines are gone!

