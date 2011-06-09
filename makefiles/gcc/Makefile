#
# Makefile for json-cpp
#

# set compiler and linker
CC = g++
LD = g++

# binaries and folders
#VERSION = `cat version`
VERSION = 0.6
LIBDIR = lib
LIBNAME = libjsoncpp-$(VERSION).so
LIB = $(LIBDIR)/$(LIBNAME)
STATIC = $(LIBDIR)/libjsoncpp-$(VERSION).a

# set library and include paths
INCLUDE =  -Iinclude -I/usr/local/include

# set compiler and linker flags
CCFLAGS = -fPIC -O3 -W -Wall
LDFLAGS = -W -Wall -L/usr/local/lib

# source files
SRCS =  $(wildcard src/lib_json/*.cpp)

# dependencies
# object files
OBJS = $(SRCS:.cpp=.o)

# dynamic lib rule
dynamiclibrary: $(OBJS) $(LIBDIR)
	# W: libjsoncpp: package-name-doesnt-match-sonames libjsoncpp-0.6
	$(LD) $(LDFLAGS) -shared -Wl,-soname,$(LIBNAME) -o $(LIB) $(OBJS)
	
	# W: libjsoncpp: shlib-without-versioned-soname usr/lib/libjsoncpp-0.6.so libjsoncpp.so
	#$(LD) $(LDFLAGS) -shared -Wl,-soname,libjsoncpp.so -o $(LIB) $(OBJS)

# static lib rule
staticlibrary: $(OBJS) $(LIBDIR)
	ar rcs $(STATIC) $(OBJS)

# compile rule
.cpp.o:
	$(CC) $(CCFLAGS) $(INCLUDE) -c $<  -o $@

$(LIBDIR):
	@mkdir -p $(LIBDIR)

# tasks
.PHONY:  clean

clean:
	@rm -rf src/lib_json/*.o
	@rm -rf lib

install:
	install -m 755 -g root -o root -d $(DESTDIR)/usr/lib
	install -m 644 -g root -o root -s $(LIB) $(DESTDIR)/usr/lib
	
	install -m 755 -g root -o root -d $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/json.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/autolink.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/value.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/reader.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/writer.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/features.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/config.h $(DESTDIR)/usr/include/json
	install -m 644 -g root -o root include/json/forwards.h $(DESTDIR)/usr/include/json

