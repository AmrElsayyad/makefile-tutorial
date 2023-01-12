`clean` is often used as a target that removes the output of other targets, but it is not a special word in Make. You can run `make` and `make clean` on this to create and delete `some_file`.

Note that `clean` is doing two new things here:

- It's not the default target, and not a prerequisite, i.e., it'll never run unless you explicitly call `make clean`.
- It's not intended to be a filename. If you happen to have a file named clean, this target won't run. 
  > See [Phony Targets](https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX025%20-%20Phony%20Targets) later in this tutorial on how to fix this.

```make
some_file: 
	touch some_file

clean:
	rm -f some_file
```

<p align="right">
  <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX005%20-%20Variables">
  	Next: EX005 - Variables
  </a>
</p>
