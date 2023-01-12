all: one two
	echo all

one:
	# This error will cause 'make' to fail and stop.
	false

	echo one

two:
	# This error will be printed but ignored, and 'make' will continue to run
	-false

	echo two

