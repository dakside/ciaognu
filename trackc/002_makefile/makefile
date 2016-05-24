CFLAGS = -g -Wall -O3
LDLIBS=
CC=c99
BIN_FILE=myprog
SOURCE_FILES=source.c

all:
	@echo "Please use 'make build' to build application and 'make clean' to clean up"

build: $(SOURCE_FILES)
	$(CC) -o $(BIN_FILE) $(CFLAGS) $(SOURCE_FILES)
	@echo "Type './myprog' to run the compiled application"
clean:
	rm source.c~ makefile~ $(BIN_FILE)
