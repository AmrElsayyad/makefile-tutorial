### The vpath Directive
Use vpath to specify where some set of prerequisites exist. The format is: 

`vpath <pattern> <directories, space/colon separated> <pattern>`

You can also do this globallyish with the variable `VPATH`

```make
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
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX025%20-%20.PHONY" id="EX025">
		Next: EX025 - .PHONY
	</a>
</p>
