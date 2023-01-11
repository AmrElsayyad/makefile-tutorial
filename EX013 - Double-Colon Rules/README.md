Double-Colon Rules are rarely used, but allow multiple rules to be defined for the same target. If these were single colons, a warning would be printed and only the second set of commands would run.

```make
all: blah

blah::
	echo "hello"

blah::
	echo "hello again"
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX014%20-%20Command%20Silencing" id="EX014">
		Next: EX014 - Command Silencing
	</a>
</p>
