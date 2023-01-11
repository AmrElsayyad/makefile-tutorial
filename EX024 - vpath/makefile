vpath %.h headers other-directory

some_binary: headers blah.h
	touch some_binary

headers:
	mkdir headers

blah.h:
	touch headers/blah.h

clean:
	rm -rf headers
	rm -f some_binary
