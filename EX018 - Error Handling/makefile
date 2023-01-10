# Add -k when running make to continue running even in the face of errors. Helpful if you want to see all the errors of Make at once.
# Add a - before a command to suppress the error
# Add -i to make to have this happen for every command.

all: one two
	echo all

one:
	# This error will cause make to fail and stop.
	false

	echo one

two:
	# This error will be printed but ignored, and make will continue to run
	-false

	echo two

