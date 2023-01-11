There are many [automatic variables](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html) but often only a few show up:

```make
hey: one two
	# Outputs "hey", since this is the target name
	echo $@

	# Outputs all prerequisites newer than the target
	echo $?

	# Outputs all prerequisites
	echo $^

	# Outputs the first prerequisite
	echo $<

	touch hey

one:
	touch one

two:
	touch two

clean:
	rm -f hey one two
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX007%20-%20Targets" id="EX007">
		Next: EX007 - Targets
	</a>
</p>
