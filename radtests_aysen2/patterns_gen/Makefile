SHELL := /bin/bash


# default compiler settings
CC = g++
OPT = -O3 -std=c++0x
LDFLAGS = -lm

# set pattern conversion name
Convert_EXE = pattern_convert.exe
Convert_SRC = pattern_convert.cc
Convert_OBJ = pattern_convert.o

#set pattern generation
Gen_EXE = pattern_generation_tmbc.exe
Gen_SRC = PatternGen.cc CSCConstants.h
Gen_OBJ = pattern_generation.o

#set pattern generation
GEM_EXE = GEMpattern_generation.exe
GEM_SRC = GEMPatternGen.cc CSCConstants.h
GEM_OBJ = GEMpattern_generation.o

# compilation for runs
all: convert generate GEMGen 
 convert:
	$(CC) -g $(OPT) $(Convert_SRC) -o $(Convert_EXE) $(LDFLAGS)
	/bin/rm -rf *.o

 generate:
	$(CC) -g $(OPT) $(Gen_SRC) -o $(Gen_EXE) $(LDFLAGS)
	/bin/rm -rf *.o

 GEMGen:
	$(CC) -g $(OPT) $(GEM_SRC) -o $(GEM_EXE) $(LDFLAGS)
	/bin/rm -rf *.o

clean:
	rm -rf *.o $(Convert_EXE) $(Gen_EXE) $(GEM_EXE)
