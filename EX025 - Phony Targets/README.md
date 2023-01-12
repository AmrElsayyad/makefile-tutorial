### Phony Targets

A _phony target_ is one that is not really the name of a file; rather it is just a name for a recipe to be executed when you make an explicit
request.  There are two reasons to use a _phony target_: to avoid a conflict with a file of the same name, and to improve performance.

If you write a rule whose recipe will not create the target file, the recipe will be executed every time the target comes up for remaking.

Here is an example:

```make
clean:
        rm *.o temp
```

Because the `rm` command does not create a file named `clean`, probably no such file will ever exist.  Therefore, the `rm` command will be executed every time you say `make clean`.

In this example, the `clean` target will not work properly if a file named `clean` is ever created in this directory. Since it has no prerequisites, `clean` would always be considered up to date and its recipe would not be executed.  To avoid this problem you
can explicitly declare the target to be phony by making it a prerequisite of the special target `.PHONY`
(see [Special Built-in Target Names](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html)) as follows:

```make
some_file:
	touch some_file
	touch clean

.PHONY: clean
clean:
	rm -f some_file
	rm -f clean
```

Once this is done, `make clean` will run the recipe regardless of whether there is a file named `clean`.

Prerequisites of `.PHONY` are always interpreted as literal target names, never as patterns (even if they contain `%` characters). To always rebuild a pattern rule consider using a
_force target_ (see [Rules without Recipes or Prerequisites](https://www.gnu.org/software/make/manual/html_node/Force-Targets.html)).

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/Makefile%20Cookbook" id="cookbook">
		Next: Makefile Cookbook
	</a>
</p>
