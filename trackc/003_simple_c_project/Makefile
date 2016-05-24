# Project information
export codename    = uberapp
export version     = 0.1
export package     = $(codename)
export distdir     = $(package)-$(version)

# Build related
export sourcedir   = src
export builddir    = build
export headerdir   = $(sourcedir)

# Install related
export prefix      = /usr/local
export exec_prefix = $(prefix)
export bindir      = $(prefix)/bin

# Tools related
export CC          ?= gcc
export CFLAGS      ?= -I $(headerdir) 

all: clean prepare compile

compile:
	$(CC) $(CFLAGS) -c -o $(builddir)/uberlib.o $(sourcedir)/uberlib.c
	$(CC) $(CFLAGS) -o $(builddir)/$(codename) $(sourcedir)/main.c $(builddir)/uberlib.o

clean: FORCE
	-rm -r $(builddir)  &>/dev/null

prepare:
	@echo prepare
	-mkdir $(builddir)

dist: $(distdir).tar.gz

$(distdir).tar.gz: FORCE $(distdir)
	tar chof - $(distdir) | gzip -9 -c >$(distdir).tar.gz
	rm -rf $(distdir)

$(distdir):
	mkdir -p $(distdir)/src
	cp Makefile $(distdir)
	cp README.txt $(distdir)
	cp src/main.c $(distdir)/src
	cp src/uberlib.c $(distdir)/src
	cp src/uberlib.h $(distdir)/src

distcheck: $(distdir).tar.gz
	gzip -cd $+ | tar xvf -
	$(MAKE) -C $(distdir) all check
	$(MAKE) -C $(distdir) DESTDIR=$${PWD}/$(distdir)/_inst install uninstall
	$(MAKE) -C $(distdir) clean
	rm -rf $(distdir)
	@echo "*** Package $(distdir).tar.gz is ready for distribution."

FORCE:
	-rm -rf $(distdir) &>/dev/null
	-rm $(distdir).tar.gz &>/dev/null

.PHONY: FORCE all clean prepare check dist distcheck install uninstall

check: compile
	$(builddir)/$(codename) | grep "Ciao from main!"
	@echo "*** All TESTS PASSED"

install:
	install -d $(DESTDIR)$(bindir)
	install -m 0755 $(builddir)/$(codename) $(DESTDIR)$(bindir)

uninstall:
	-rm $(DESTDIR)$(bindir)/$(codename) &>/dev/null
