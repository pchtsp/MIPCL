CC=g++
ARC=-mfpmath=sse -msse2
CFLAGS=-c -std=c++17 -fno-rtti -O3 $(ARC) -I$(HDR_MIPSHELL) -I$(HDR_MIPCL)
LDFLAGS=-shared-libgcc
INSDIR=../bin
INS=install
MIP_DIR=$(MIPCLDIR)
RM=rm -f
CFLAGS+=-DMIPSHELL_API="" -DMIP_API=""
LDFLAGS+= -L$(MIP_DIR)/lib -lmipcl -lmipshell
TARGET=dea
#
HDR_MIPCL=$(MIP_DIR)/mipcl/headers
HDR_MIPSHELL=$(MIP_DIR)/mipshell/headers
#
VPATH=../sources
CFLAGS+=-I$(VPATH)
MOD= $(shell echo $(VPATH)/*.mod)
XYZ=$(MOD:.mod=.aux)
SRC=$(notdir $(shell echo $(VPATH)/*.cpp))
OBJS=$(SRC:.cpp=.o)
#
.cpp.o:
	$(CC) $(CFLAGS) $< -o $@
%.aux : %.mod ;	$(MIP_DIR)/bin/mod2cpp $< $(<D)/$@
#
build: $(OBJS) 
	$(CC) $(LDFLAGS) $(OBJS) -o $(TARGET)
#dependencies
dea.cpp: dea.mod 
dea.o: dea.cpp dea.aux dea.h
main.o: main.cpp dea.h
#
.PHONY: clean
clean:
	$(RM) $(OBJS) $(XYZ)
install: $(TARGET)
	$(INS) $(TARGET) $(INSDIR)
	$(RM) $(TARGET)
all: build install

