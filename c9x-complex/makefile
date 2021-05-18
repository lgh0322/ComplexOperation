# Makefile for C9X complex variables library
# Edit endian-ness and computer type properly in mconf.h before compiling.
# For additional test programs see also celefunt.mak.

# Caution: the tests contain some references to the cephes math library
# or references to standard float or long double functions that might
# not be available.
# This should be enough to run at least the double precision functions:
LIBS = stubs.o -lm
# These are intended to get the cephes libraries:
#LIBS = -lml -lmd -lmf
#LIBS = ../libml.a ../libmd.a ../libmf.a

CC = mingw32-gcc
#CC = /b/gnu/gcc-build/gcc/xgcc -B/b/gnu/gcc-build/gcc/ -I/b/gnu/gcc-build/gcc
# For 128-bit wide long double
#PRECFLAGS = -DLD128BITS
PRECFLAGS = 
CFLAGS = $(PRECFLAGS) -I. -g -O0 -Wall
#CFLAGS = $(PRECFLAGS) -I. -g -O1 -Wall
#CFLAGS = $(PRECFLAGS) -I. -g -O0 -Wall

# float precision
SFILES = cmplxf.o clogf.o cgammaf.o
# double precision
DFILES = cmplx.o clog.o cgamma.o
# long double precision

LFILES = cmplxl.o clogl.o cgammal.o
LIBMCFILES = $(SFILES) $(DFILES) $(LFILES)


all: libmc.a mtst cvect dccalc mtstf mtstl whitebxf whitebx

mtst: mtst.o $(DFILES) stubs.o
	$(CC) -v -o mtst mtst.o $(DFILES) $(LIBS)

mtstf: mtstf.o $(SFILES) stubs.o
	$(CC) -o mtstf mtstf.o $(SFILES) $(LIBS)

mtstl: mtstl.o $(LFILES) stubs.o
	$(CC) -o mtstl mtstl.o $(LFILES) $(LIBS)

cvect: cvect.o clog.o cmplx.o stubs.o
	$(CC) -o cvect cvect.o clog.o cmplx.o $(LIBS)


whitebxf: whitebxf.o libmc.a
	$(CC) $(CFLAGS) -o whitebxf whitebxf.o libmc.a $(LIBS)

whitebxf.o: whitebxf.c complex.h

whitebx: whitebx.o  libmc.a
	$(CC) $(CFLAGS) -o whitebx whitebx.o libmc.a $(LIBS)

whitebx.o: whitebx.c complex.h


libmc.a: $(LIBMCFILES)
	ar rv libmc.a $(LIBMCFILES)



dccalc: dccalc.o
#	$(CC) -o dccalc dccalc.o libmc.a -lreadline -lncurses $(LIBS)
	$(CC) -o dccalc dccalc.o libmc.a $(LIBS)

dccalc.o: dccalc.c dccalc.h
#	$(CC) $(CFLAGS) -DUSE_READLINE=1 -c dccalc.c
	$(CC) $(CFLAGS) -c dccalc.c

clog.o: clog.c complex.h protos.h
cmplx.o: cmplx.c complex.h protos.h
clogf.o: clogf.c complex.h protos.h
cmplxf.o: cmplxf.c complex.h protos.h
clogl.o: clogl.c complex.h protos.h
cmplxl.o: cmplxl.c complex.h protos.h
