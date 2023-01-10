# Adding .PHONY to a target will prevent Make from confusing the phony target with a file name.
# In this example, if the file clean is created, make clean will still be run.
# Technically, I should have have used it in every example with all or clean, but I didn't to keep the examples clean.
# Additionally, "phony" targets typically have names that are rarely file names, and in practice many people skip this.

some_file:
	touch some_file
	touch clean

.PHONY: clean

clean:
	rm -f some_file
	rm -f clean
