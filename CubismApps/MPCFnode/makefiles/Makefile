include ../../Makefile.config

#########

VPATH := ../source/ ../../MPCFcore/source/ ../../../Cubism/source/
.DEFAULT_GOAL := mpcf-node

OBJECTS = main.o FlowStep_LSRK3.o Test_SteadyState.o Test_ShockBubble.o  Types.o Test_SIC.o Test_Cloud.o WaveletCompressor.o
OBJECTS += ../../MPCFcore/makefiles/Convection_CPP.o ../../MPCFcore/makefiles/Update.o ../../MPCFcore/makefiles/MaxSpeedOfSound.o 

ifeq "$(qpx)" "1"
	OBJECTS += ../../MPCFcore/makefiles/WenoSOA2D_QPX.o
	OBJECTS += ../../MPCFcore/makefiles/HLLESOA2D_QPX.o
	OBJECTS += ../../MPCFcore/makefiles/DivSOA2D_QPX.o
endif

ifeq "$(qpxemu)" "1"
	OBJECTS += ../../MPCFcore/makefiles/WenoSOA2D_QPX.o
	OBJECTS += ../../MPCFcore/makefiles/HLLESOA2D_QPX.o
	OBJECTS += ../../MPCFcore/makefiles/DivSOA2D_QPX.o
endif

OBJECTS += Profiler.o 


#on brutus flowstep performs better without native arch
ifeq "$(findstring brutus,$(shell hostname))" ""
	FSDIEGOEXTRA=$(extra)
endif

all: mpcf-node

mpcf-node: $(OBJECTS)
	$(CC) $(OPTFLAGS) $(CPPFLAGS) $^ -o $@ $(LIBS)

WaveletCompressor.o: WaveletCompressor.cpp
#	$(CC) $(OPTFLAGS) $(CPPFLAGS) -c $^ -o $@
	$(CC) $(OPTFLAGS) $(CPPFLAGS)  -c $^ -o $@

%.o: %.cpp
	$(CC)  $(OPTFLAGS) $(CPPFLAGS) -c $^ -o $@

../../MPCFcore/makefiles/%.o: %.cpp
	$(CC)  $(OPTFLAGS) $(CPPFLAGS) -c $^ -o $@

clean:
	rm -f *.o mpcf-node

cleanall:
	(cd ../../MPCFcore/makefiles; make clean)
	make clean;
