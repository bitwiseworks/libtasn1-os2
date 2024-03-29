## Process this file with automake to produce Makefile.in
# Copyright (C) 2002-2014 Free Software Foundation, Inc.
#
# This file is part of LIBTASN1.
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

VENDOR ?=community
BUILD_INFO=\#\#1\#\# $(shell date +'%d %b %Y %H:%M:%S')     $(shell uname -n)
BUILDLEVEL_INFO=@\#$(VENDOR):$(VERSION)\#@$(BUILD_INFO)::::0::

SUBDIRS = gl

AM_CFLAGS = $(WARN_CFLAGS) $(WERROR_CFLAGS) $(CFLAG_VISIBILITY) $(CODE_COVERAGE_CFLAGS)
AM_CPPFLAGS = -I$(builddir)/gl -I$(srcdir)/gl -I$(builddir)/includes -I$(srcdir)/includes\
 -DASN1_BUILDING $(CODE_COVERAGE_CPPFLAGS)

include_HEADERS = includes/libtasn1.h

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libtasn1.pc

lib_LTLIBRARIES = libtasn1.la

libtasn1_la_SOURCES =	\
	ASN1.y		\
	coding.c	\
	decoding.c	\
	element.c	\
	element.h	\
	errors.c	\
	gstr.c		\
	gstr.h		\
	int.h		\
	includes/libtasn1.h	\
	libtasn1.map	\
	parser_aux.c	\
	parser_aux.h	\
	structure.c	\
	structure.h	\
	version.c

libtasn1_la_LIBADD = gl/libgnu.la

libtasn1_la_LDFLAGS = \
	-no-undefined \
	-version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE) \
	-buildlevel '$(BUILDLEVEL_INFO)' \
	$(CODE_COVERAGE_LDFLAGS)

if HAVE_LD_VERSION_SCRIPT
libtasn1_la_LDFLAGS += -Wl,--version-script=$(srcdir)/libtasn1.map
else
libtasn1_la_LDFLAGS += -export-symbols-regex '^(asn1|libtasn1_).*'
endif
