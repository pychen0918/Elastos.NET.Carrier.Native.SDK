PREFIX ?= /usr/local
INCLUDE_PATH ?= include
LIBRARY_PATH ?= lib

INSTALL_INCLUDE_PATH = $(DESTDIR)$(PREFIX)/$(INCLUDE_PATH)
INSTALL_LIBRARY_PATH = $(DESTDIR)$(PREFIX)/$(LIBRARY_PATH)

INSTALL ?= cp -a

CFLAGS := $(CFLAGS) -I$(INSTALL_INCLUDE_PATH) -I../../src/common  -fPIC -Wall  -Wstrict-prototypes -Wwrite-strings

LIBS := $(LIBS) -lIOEXcommon -lIOEXcarrier -lIOEXsession -lncurses -lconfig

ifeq (, $(findstring $(HOST), Darwin iOS))
	LDFLAGS = -Wl,-rpath-link=$(INSTALL_LIBRARY_PATH)
	LIBS := $(LIBS) -lpthread
endif

OBJS = shell.o config.o

.PHONY: all clean install

all: IOEXshell

IOEXshell: $(OBJS)
	$(CC) -o $@ $(OBJS) $(LDFLAGS) -L$(INSTALL_LIBRARY_PATH) $(LIBS)

.c.o:
	$(CC) -c $(CFLAGS) -o $@ $<

install: all

clean:
	rm -rf IOEXshell *.o

