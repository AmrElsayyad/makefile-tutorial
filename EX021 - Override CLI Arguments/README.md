### Command line arguments and override

You can override variables that come from the command line by using override.

Run with `make option_one=hi option_two=bye`

```make
# Overrides command line arguments
override option_one = did_override

# Does not override command line arguments
option_two = not_override

all: 
	echo $(option_one)
	echo $(option_two)
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX022%20-%20Functions" id="EX022">
		<img src="https://img.shields.io/badge/Next-EX022: Functions-blue.svg">
	</a>
</p>
