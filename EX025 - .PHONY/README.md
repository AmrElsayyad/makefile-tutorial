Adding `.PHONY` to a target will prevent Make from confusing the phony target with a file name. 

In this example, if the file clean is created, make clean will still be run. 

> Technically, I should have have used it in every example with all or clean, but I didn't to keep the examples clean. Additionally, "phony" targets typically have names that are rarely file names, and in practice many people skip this.

```make
some_file:
	touch some_file
	touch clean

.PHONY: clean

clean:
	rm -f some_file
	rm -f clean
```

<p align="right">
	<a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX026%20-%20.DELETE_ON_ERROR" id="EX026">
		Next: EX026 - .DELETE_ON_ERROR
	</a>
</p>
