# Copyright 2015 University Corporation for Atmospheric Research
#
# This file is part of the LDM package.  See the file COPYRIGHT
# in the top-level source-directory of the package for copying and
# redistribution conditions.
#
## Process this file with automake to produce Makefile.in

include_HEADERS		= ulog.h
noinst_LTLIBRARIES	= lib.la
lib_la_SOURCES		= ulog.c
dist_man3_MANS		= ulog.3

check_PROGRAMS		= test_gmtime test0
TESTS			= test_gmtime

test_gmtime_SOURCES	= test_gmtime.c
test_gmtime_LDADD	= lib.la

test0_SOURCES	= ulog.c
test0_CPPFLAGS	= -DTEST0

check-local: test0
	./test0 -l- 2>/dev/null
