files := file1 file2
a := \nOne Two\n	# a is assigned to the string "one two"
b := '\nOne Two\n'	# Not recommended. b is assigned to the string "'one two'"

all: some_file
	printf ${a}
	printf '${a}'
	printf ${b}
	printf '${b}'

some_file: ${files}
	echo "Look at this variable: " ${files}
	touch some_file

file1:
	touch file1

file2:
	touch file2

clean:
	rm -f file1 file2 some_file
