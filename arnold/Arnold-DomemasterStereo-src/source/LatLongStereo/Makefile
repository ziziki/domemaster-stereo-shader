# Linux - LatLongStereo Arnold Shader Makefile
# by Andrew Hazelden  andrew@andrewhazelden.com
# http://www.andrewhazelden.com

# You can compile this file from the command line using:
# make -f Makefile

# You can install the files using the command
# make -f Makefile install

CC=g++

# Which version of Maya you are running with Arnold?
#MAYA_VERSION=2012
#MAYA_VERSION=2013
# Current Build Version = 2014
MAYA_VERSION=2014
#MAYA_VERSION=2015

MTOA_SHADERS_DIR=$(HOME)/solidangle/mtoa/$(MAYA_VERSION)/shaders
MTOA_TEMPLATE_DIR=$(HOME)/solidangle/mtoa/$(MAYA_VERSION)/scripts/mtoa/ui/ae

# Which version of the Arnold API Devkit are you using?
MTOA_API_VERSION=4.2.3.1

MTOA_DEV_DIR=$(HOME)/solidangle/Arnold-$(MTOA_API_VERSION)-linux
MTOA_INCLUDE_DIR=$(MTOA_DEV_DIR)/include

INC = -I$(MTOA_INCLUDE_DIR)/
LIB =
LIB_STATIC = 
CFLAGS = -c -O3 -fPIC -Bsymbolic -DBIT64
LIBTOOL = ld
LDEXECFLAGS=

OBJS = LatLongStereo.o
SRCS = LatLongStereo.cpp

all: LatLongStereo.so

$(OBJS): 
	$(CC) $(CFLAGS) $(INC) $(LIB) $(SRCS) $(LIB_STATIC)

LatLongStereo.so : $(OBJS) 
	$(LIBTOOL) -export-dynamic -shared $(LDEXECFLAGS) -o LatLongStereo.so $(OBJS)

clean: 
	rm -f $(OBJS) 
	rm -f LatLongStereo.so

install:
	# Arnold Shader and Metadata File
	# ---------------------------------
	cp ./LatLongStereo.so $(MTOA_SHADERS_DIR)
	cp ./LatLongStereo.mtd $(MTOA_SHADERS_DIR)

	# Arnold Maya AE Template File
	# ------------------------------
	cp ./LatLongStereoTemplate.py $(MTOA_TEMPLATE_DIR)
	
go: clean all install
