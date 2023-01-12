CC := gcc

objects = foo.o bar.o all.o
all: $(objects)

# Define a pattern rule that compiles every .c file into a .o file
%.o : %.c
		$(CC) -c $(CFLAGS) $(CPPFLAGS) $< -o $@

all.c:
	echo 'int main() { return 0; }' > $@

# Define a pattern rule that has no pattern in the prerequisites.
# This just creates a return 0 .c files when needed.
%.c:
	touch $@

clean:
	rm -f *.c *.o *.exe
