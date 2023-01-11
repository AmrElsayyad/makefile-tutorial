# blah requires blah.o, so make searches for the blah.o target
blah.exe: blah.o
	gcc blah.o -o blah.exe				# Runs third

# blah.o requires blah.c, so make searches for the blah.c target
blah.o: blah.c
	gcc -c blah.c -o blah.o				# Runs second

# blah.c has no dependencies, so the echo command is run
blah.c:
	echo "int main() { return 0; }" > blah.c	# Runs first
