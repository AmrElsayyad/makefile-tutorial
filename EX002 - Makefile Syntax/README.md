A Makefile consists of a set of rules. A rule generally looks like this:

```make
targets: prerequisites
	command
	command
	command
```

- The _targets_ are file names, separated by spaces. Typically, there is only one per rule.
- The _commands_ are a series of steps typically used to make the target(s). These need to start with a tab character, not spaces.
- The _prerequisites_ are also file names, separated by spaces. These files need to exist before the commands for the target are run. These are also called _dependencies_.

<p align="right">
  <a href="https://github.com/AmrElsayyad/makefile-tutorial/tree/main/EX003%20-%20Makefile%20Sequence%20of%20Events">
  	Next: EX003 - Makefile Sequence of Events
  </a>
</p>
