# Copyright 2011 University Corporation for Atmospheric Research
#
# This file is part of the Unidata LDM package.  See the file COPYRIGHT in the
# top-level source-directory of the package for copying and redistribution
# conditions.
#
## Process this file with automake(1) to produce file Makefile.in

################################################################################

LDMHOME			= @LDMHOME@
LDMSRC			= $(top_srcdir)
SUDO			= @SUDO@
SU			= @SU@

CLEANFILES		= $(BUILT_SOURCES)

CPPFLAGS		= \
	-DLDM_SUPPORT \
	-I$(top_srcdir) \
	-I$(top_srcdir)/noaaport \
	-I$(top_srcdir)/protocol -I$(top_builddir)/protocol \
	-I$(top_srcdir)/protocol2 \
	-I$(top_srcdir)/pq \
	-I$(top_srcdir)/ulog \
	-I$(top_srcdir)/log \
	-I$(top_srcdir)/misc \
	-I$(top_srcdir)/registry \
	@CPPFLAGS@

bin_PROGRAMS		= fileIngester

EXTRA_DIST              = \
	datelib.hin \
	stdclib.hin \
	goesr_lib.hin \
	mlogger.hin

BUILT_SOURCES		= \
	datelib.h \
	stdclib.h \
	goesr_lib.h \
	mlogger.h

COMMON_SOURCES		= \
	stdclib.c stdclib.h \
	goesr_lib.c goesr_lib.h \
	mlogger.c mlogger.h \
	datelib.c datelib.h \
	ldmProductQueue.c ldmProductQueue.h

fileIngester_SOURCES		= fileIngester.c $(COMMON_SOURCES)

LDADD 			= $(top_builddir)/lib/libldm.la

TAGS_FILES		= \
	*.c *.h

.c.i:
	$(COMPILE) -E $< >$@

.hin.h:
	./extractDecls $*.hin $*.c >$@.tmp
	mv -f $@.tmp $@

#installcheck-local:
#	pqcreate -c -s 2m /tmp/readnoaaport-test.pq
#	$(DESTDIR)$(bindir)/readnoaaport -l- -q /tmp/readnoaaport-test.pq \
#	    $(srcdir)/nwstgdump.data
#	rm /tmp/readnoaaport-test.pq

#check-local:		check-readnoaaport
#check-readnoaaport:	readnoaaport
#	pqcreate -c -s 2m /tmp/readnoaaport-test.pq
#	./readnoaaport -nl- -q /tmp/readnoaaport-test.pq \
#	    $(srcdir)/nwstgdump.data
#	rm /tmp/readnoaaport-test.pq

#root-ni-ck:
#	./noaaportIngester -b 3 -q /tmp/noaaportIngester-test.pq \
#	    <$(srcdir)/nwstgdump.data

#valgrind:		valgrind-readnoaaport

#valgrind-readnoaaport:		readnoaaport
#	pqcreate -c -s 2m /tmp/readnoaaport-test.pq
#	$(LIBTOOL) --mode=execute valgrind --leak-check=yes \
#	    readnoaaport -l- -q /tmp/readnoaaport-test.pq nwstgdump.data
#	rm /tmp/readnoaaport-test.pq

sudo:
if HAVE_SUDO
	$(SUDO) $(MAKE) $(AM_MAKEFLAGS) $(TARGET) 2>/dev/tty
else
if HAVE_SU
	@printf "Enter root's password (or don't): " >/dev/tty
	@$(SU) root -c 'PATH='$$PATH' $(MAKE) $(AM_MAKEFLAGS) $(TARGET)' \
	    </dev/tty 2>/dev/tty
	@echo >/dev/tty
endif
endif
	
#valgrind-noaaportIngester:	noaaportIngester
#	pqcreate -c -s 2m /tmp/noaaportIngester-test.pq
#	$(MAKE) $(AM_MAKEFLAGS) sudo TARGET=root-ni-vg
#	rm /tmp/noaaportIngester-test.pq

#root-ni-vg:
#	$(LIBTOOL) --mode=execute valgrind --leak-check=yes \
#	    noaaportIngester -n -q /tmp/noaaportIngester-test.pq \
#		<$(srcdir)/nwstgdump.data

#debug-readnoaaport:	readnoaaport
#	pqcreate -c -s 2m /tmp/readnoaaport-test.pq
#	echo 'handle SIGCONT pass noprint nostop' >/tmp/readnoaaport.gdb
#	echo 'b 617' >>/tmp/readnoaaport.gdb
#	echo 'run -l- -q /tmp/readnoaaport-test.pq nwstgdump.data' \
#	    >>/tmp/readnoaaport.gdb
#	$(LIBTOOL) --mode=execute gdb -x /tmp/readnoaaport.gdb readnoaaport
#	rm /tmp/readnoaaport-test.pq /tmp/readnoaaport.gdb

#debug-noaaportIngester:	noaaportIngester
#	pqcreate -c -s 2m /tmp/noaaportIngester-test.pq
#	echo 'handle SIGCONT pass noprint nostop' >/tmp/noaaportIngester.gdb
#	echo 'handle SIGTERM pass nostop' >>/tmp/noaaportIngester.gdb
#	echo 'run -q /tmp/noaaportIngester-test.pq -n -m 224.0.1.1' \
#	    >>/tmp/noaaportIngester.gdb
#	$(MAKE) $(AM_MAKEFLAGS) sudo TARGET=root-ni-db
#	rm /tmp/noaaportIngester-test.pq /tmp/noaaportIngester.gdb

#root-ni-db:
#	$(LIBTOOL) --mode=execute gdb -x /tmp/noaaportIngester.gdb \
#	      noaaportIngester

.PHONY:	\
	sudo
#	install-html \
#	root-ni-ck \
#	root-ni-db \
#	root-ni-vg \
#	sudo
