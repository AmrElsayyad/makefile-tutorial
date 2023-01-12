# Run with 'make -s' to see MAKEFLAGS working

all: ifeq_empty ifdef_expanded ifdef_not_expanded ifdef_empty flags

# ifeq

tabs =		# contains tabulations

ifeq_empty:
ifeq ($(strip ${tabs}),)
	echo "'tabs' is empty or contains only whitespace"
else
	echo "This will not run"
endif


# ifdef with expansion

var1 = true
var2 = var1

ifdef_expanded:
ifdef ${var2}
	echo "'var2' is expanded to 'var1' and 'var1' is defined"
endif


# ifdef with no expansion

var3 =
var4 = $(var3)

ifdef_not_expanded:
ifdef var4
	echo "'var4' is defined even though it is expanded value is not"
else
	echo "This will not run"
endif


# ifdef with empty value

var5 =

ifdef_empty:
ifdef var5
	echo "This will not run"
else
	echo "'var5' is not defined"
endif


# MAKEFLAGS

flags:
ifneq (,$(findstring s,$(word 1,-${MAKEFLAGS})))
	echo "s was passed to MAKEFLAGS"
endif
