# If you want a string to have a dollar sign, you can use $$.
# This is how to use a shell variable in bash or sh.

make_var = I am a make variable

all:
	# Same as running "sh_var='I am a shell variable'; echo $sh_var" in the shell
	sh_var='I am a shell variable'; echo $$sh_var

	# Same as running "echo I am a make variable" in the shell
	echo $(make_var)
