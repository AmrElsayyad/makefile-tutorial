If you want a string to have a dollar sign, you can use `$$`. This is how to use a shell variable in bash or sh. Note the differences between Makefile variables and Shell variables in this next example.

```make
make_var = I am a make variable

all:
	# Same as running "sh_var='I am a shell variable'; echo $sh_var" in the shell
	sh_var='I am a shell variable'; echo $$sh_var

	# Same as running "echo I am a make variable" in the shell
	echo $(make_var)
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX018%20-%20Error%20Handling" id="EX018">
		<img src="https://img.shields.io/badge/Next-EX018: Error Handling-blue.svg">
	</a>
</p>
