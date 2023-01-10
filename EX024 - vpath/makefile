# The vpath Directive
# Use vpath to specify where some set of prerequisites exist.
# The format is vpath <pattern> <directories, space/colon separated>
# <pattern> can have a %, which matches any zero or more characters.
# You can also do this globallyish with the variable VPATH

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

