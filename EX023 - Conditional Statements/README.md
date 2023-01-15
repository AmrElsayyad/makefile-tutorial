### Syntax of Conditionals

The syntax of a simple conditional with no else is as follows:

```make
conditional-directive
text-if-true
endif
```

The `text-if-true` may be any lines of text, to be considered as part of the makefile if the condition is true. If the condition is false, no text is used instead.

The syntax of a complex conditional is as follows:

```make
conditional-directive
text-if-true
else
text-if-false
endif
```

or:

```make
conditional-directive-one
text-if-one-is-true
else conditional-directive-two
text-if-two-is-true
else
text-if-one-and-two-are-false
endif
```

There can be as many _else conditional-directive_ clauses as necessary. Once a given condition is true, `text-if-true` is used and no other clause is used; if no condition is true then `text-if-false` is used. The `text-if-true` and `text-if-false` can be any number of lines of text.

The syntax of the _conditional-directive_ is the same whether the conditional is simple or complex; after an else or not.

There are four different ways _conditional-directives_ can test the same condition. Here is how:

```make
conditional-directive (arg1, arg2)
conditional-directive 'arg1' 'arg2'
conditional-directive "arg1" "arg2"
conditional-directive "arg1" 'arg2'
conditional-directive 'arg1' "arg2"
```

### Types of Conditional-Directives

There are four different directives that test different conditions:

- `ifeq`
  
  ```make
  ifeq (arg1, arg2)
  text-if-true
  else
  text-if-false
  endif
  ```
  
  Expand all variable references in `arg1` and `arg2` and compare them. If they are identical, the `text-if-true` is effective; otherwise, the `text-if-false`, if any, is effective.

  Often you want to test if a variable has a non-empty value. When the value results from complex expansions of variables and functions, expansions you would consider empty may actually contain whitespace characters and thus are not seen as empty. However, you can use the `strip` function (see [Functions](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX022%20-%20Functions)) to avoid interpreting whitespace as a non-empty value.

  For example:
  
  ```make
  tabs =		# contains tabulations
  
  ifeq_empty:
  ifeq ($(strip ${tabs}),)
  	echo "'tabs' is empty or contains only whitespace"
  else
  	echo "This will not run"
  endif
  ```

  will evaluate `text-if-empty` even if the expansion of `${tabs}` contains whitespace characters.

- `ifneq`
  
  ```make
  ifneq (arg1, arg2)
  text-if-true
  else
  text-if-false
  endif
  ```

  Expand all variable references in `arg1` and `arg2` and compare them. If they are different, the `text-if-true` is effective; otherwise, the `text-if-false`, if any, is effective.

- `ifdef`
  
  ```make
  ifdef variable-name
  text-if-true
  else
  text-if-false
  endif
  ```
  
  The `ifdef` form takes the name of a variable as its argument, not a reference to a variable. If the value of that variable has a non-empty value, the `text-if-true` is effective; otherwise, the `text-if-false`, if any, is effective. Variables that have never been defined have an empty value. The text `variable-name` is expanded, so it could be a variable or function that expands to the name of a variable.

  For example:

  ```make
  var1 = true
  var2 = var1
  
  ifdef_expanded:
  ifdef ${var2}
  	echo "'var2' is expanded to 'var1' and 'var1' is defined"
  endif
  ```

  The variable reference `${var2}` is expanded, yielding `var1`, which is considered to be the name of a variable. The variable `var1` is not expanded, but its value is examined to determine if it is non-empty.

  Note that `ifdef` only tests whether a variable has a value. It does not expand the variable to see if that value is nonempty. Consequently, tests using `ifdef` return true for all definitions except those like `foo =`.

  For example:

  ```make
  var3 =
  var4 = $(var3)
  
  ifdef_not_expanded:
  ifdef var4
  	echo "'var4' is defined even though it is expanded value is not"
  else
  	echo "This will not run"
  endif
  ```

  `var4` is defined, while:

  ```make
  var5 =
  
  ifdef_empty:
  ifdef var5
  	echo "This will not run"
  else
  	echo "'var5' is not defined"
  endif
  ```
  
  `var5` is not defined.

  > Note: Use this only if you want to check if a variable is assigned a value. If you want to check if a variable is empty, use the the example of `ifeq`.

- `ifndef`
  
  ```make
  ifndef variable-name
  text-if-true
  else
  text-if-false
  endif
  ```
  
  If the variable `variable-name` has an empty value, the `text-if-true` is effective; otherwise, the `text-if-false`, if any, is effective. The rules for expansion and testing of `variable-name` are identical to the ifdef directive.
  
Extra spaces are allowed and ignored at the beginning of the conditional directive line, but a tab is not allowed. (If the line begins with a tab, it will be considered part of a recipe for a rule.) Aside from this, extra spaces or tabs may be inserted with no effect anywhere except within the directive name or within an argument. A comment starting with `#` may appear at the end of the line.

Conditionals affect which lines of the makefile `make` uses. If the condition is true, `make` reads the lines of the `text-if-true` as part of the makefile; if the condition is false, `make` ignores those lines completely. It follows that syntactic units of the makefile, such as rules, may safely be split across the beginning or the end of the conditional.

`make` evaluates conditionals when it reads a makefile. Consequently, you cannot use automatic variables in the tests of conditionals because they are not defined until recipes are run (see [Automatic Variables](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX006%20-%20Automatic%20Variables)).

### Conditionals that Test Flags

You can write a conditional that tests `make` command flags such as `-s` by using the variable `MAKEFLAGS` together with the `findstring` function (see [Functions](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX022%20-%20Functions) for String Substitution and Analysis). 

Recall that `MAKEFLAGS` will put all single-letter options (such as `-s`) into the first word, and that word will be empty if no single-letter options were given. To work with this, it's helpful to add a value at the start to ensure there's a word: for example `-$(MAKEFLAGS)`.

The `findstring` function determines whether one string appears as a substring of another. If you want to test for the `-s` flag, use `s` as the first string and the first word of `MAKEFLAGS` as the other.

For example:


```make
flags:
ifneq (,$(findstring s,$(word 1,-${MAKEFLAGS})))
	echo "s was passed to MAKEFLAGS"
endif
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX024%20-%20VPATH_%20Search%20Path%20for%20All%20Prerequisites" id="EX024">
		<img src="https://img.shields.io/badge/Next-EX024: VPATH_ Search Path for All Prerequisites-blue.svg">
	</a>
</p>
