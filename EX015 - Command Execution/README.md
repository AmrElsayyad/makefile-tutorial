Each command is run in a new shell (or at least the effect is as such).

```make
all: 
	cd ..
	# The cd above does not affect this line,
	# because each command is effectively run in a new shell
	echo `pwd`

	# This cd command affects the next because they are on the same line
	cd ..; echo `pwd`

	# Same as above
	cd ..; \
	echo `pwd`
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX016%20-%20Default%20Shell" id="EX016">
		Next: EX016 - Default Shell
	</a>
</p>
