# Make selects the target blah.exe, because the first target is the default target
# blah requires blah.o, so make searches for the blah.o target
blah.exe: blah.o
	gcc blah.o -o blah.exe				# Runs third

# blah.o requires blah.c, so make searches for the blah.c target
blah.o: blah.c
	gcc -c blah.c -o blah.o				# Runs second

# blah.c has no dependencies, so the echo command is run
blah.c:
	echo "int main() { return 0; }" > blah.c	# Runs first

# The commands for target blah.o is then run, because all of the blah.o dependencies are finished
# Finally, the commands for target blah.exe is run, because all the blah.exe dependencies are finished
# That's it: blah.exe is a compiled c program
