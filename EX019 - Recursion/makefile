# To recursively call a makefile, use the special $(MAKE) instead of 'make' because it will pass the make flags for you and won't itself be affected by them.

new_contents = "hello:\n\ttouch inside_file"

all:
	mkdir -p subdir
	printf ${new_contents} > subdir/makefile
	cd subdir && ${MAKE}

clean:
	rm -rf subdir
