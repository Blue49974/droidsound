BINDIR = /usr/local/bin
XMMSPLUGINDIR= 

ARCHFLAGS=
CC=gcc
OBJCOPY=objcopy
DEBUGFLAGS=-g
XMMSFLAGS=
XMMSLIBS=
SHAREDLIBRARYFLAGS=-fPIC -shared
CFLAGS = -Wall -O2 $(SHAREDLIBRARYFLAGS) $(DEBUGFLAGS) $(XMMSFLAGS) $(ARCHFLAGS) -I../common -I../../include
CLIBS = $(XMMSLIBS) -lm

all:	libuade2.so

include ../common/Makefile.common

MODULES = plugin.o subsongseek.o fileinfo.o $(COMMONMODULES)

libuade2.so:	$(MODULES)
	$(CC) $(CFLAGS) -o $@ $(MODULES) $(CLIBS)
	$(OBJCOPY) -G get_iplugin_info $@

install:	libuade2.so
	mkdir -p "$(XMMSPLUGINDIR)" "$(BINDIR)"
	install libuade2.so "$(XMMSPLUGINDIR)"
	install uadexmmsadd "$(BINDIR)"/

fileinfo.o:	fileinfo.c fileinfo.h
	$(CC) $(CFLAGS) -c $<

plugin.o:	plugin.c plugin.h subsongseek.h fileinfo.h  ../common/uadecontrol.h ../../include/uadeipc.h ../../include/uadeconstants.h subsongseek.h ../common/effects.h ../common/md5.h $(PLAYERHEADERS)
	$(CC) $(CFLAGS) -c $<

subsongseek.o:	subsongseek.c subsongseek.h plugin.h
	$(CC) $(CFLAGS) -c $<

clean:	
	rm -f *.so *.o
