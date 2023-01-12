vpath %.h headers
vpath %.c src

some_binary: headers blah.h src blah.c
	touch some_binary

headers:
	mkdir headers

blah.h:
	touch headers/blah.h

src:
	mkdir src

blah.c:
	touch src/blah.c

clean:
	rm -rf headers
	rm -rf src
	rm -f some_binary
