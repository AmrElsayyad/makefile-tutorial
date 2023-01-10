# The make tool will stop running a rule (and will propogate back to prerequisites) if a command returns a nonzero exit status.
# DELETE_ON_ERROR will delete the target of a rule if the rule fails in this manner.
# This will happen for all targets, not just the one it is before like PHONY.
# It's a good idea to always use this, even though make does not for historical reasons.

.DELETE_ON_ERROR:

all: one two

one:
	touch one
	false

two:
	touch two
	false

