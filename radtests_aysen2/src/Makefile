
default: all

####### Compiler, tools and options

# Where is Qt installed?
QTDIR        = /usr
#QTDIR        = /rooms/trunk/cooljoe/Qt/qt-everywhere-opensource-src-4.7.2
#QTDIR        = /home/cooljoe/Qt/qt-everywhere-opensource-src-4.7.2
#QTDIR        = /usr/local/Trolltech/Qt-4.7.2
#QTDIR        = /usr

MOC          = /usr/lib64/qt4/bin/moc
#MOC          = /usr/bin/moc-qt4

CXX		= g++
DEFINES		= -DQT_NO_DEBUG -DQT_GUI_LIB -DQT_CORE_LIB
CXXFLAGS	= -Wall -pipe -O1 -W -D_REENTRANT $(DEFINES)
INCPATH		= -I../include -I$(QTDIR)/mkspecs/default -I$(QTDIR)/include/QtCore -I$(QTDIR)/include/QtGui -I$(QTDIR)/include
LINK		= g++
LFLAGS		= -Wall -Wl,-O1 -Wl,-rpath,$(QTDIR)/lib
LIBS		= -L$(QTDIR)/lib -lQtGui -lQtCore -lpthread 



####### Files

ETHHEADERS 	= \
		../include/eth.h \
		../include/debug.h \
		../include/eth_lib.h \
		../include/utils.h \
		../include/commands.h 

ETHSRC	= \
		eth_lib.cpp \
		utils.cpp \
		commands.cpp 

ETHOBJ = $(ETHSRC:.cpp=.o)

COMSRC 	= \
		makepattern.cpp \
		looptest.cpp \
		looptest2.cpp \
		dumpHEX.cpp \
		sendpat.cpp \
		reset.cpp \
		read_and_check.cpp \
		test_command.cpp \
		send_command.cpp \
		receive_command.cpp \
		send_receive.cpp \
		send.cpp \
		read.cpp \
		send_0.cpp \
		send_d.cpp \
		send_e.cpp

COMOBJ = $(COMSRC:.cpp=.o)
COMEXE = $(COMSRC:.cpp=.exe)

GUIOBJ	= \
		RadTestThread.o \
		RadTestWorker.o \
		RadTestGUI.o \
		QProgressIndicator.o \
		moc_RadTestThread.o \
		moc_RadTestWorker.o \
		moc_RadTestGUI.o \
		moc_QProgressIndicator.o

GUIEXE	=	RadTestGUI.exe



####### Build rules

all: 	$(ETHOBJ) $(COMEXE) $(GUIEXE)


clean: 	FORCE
	rm $(ETHOBJ) $(GUIOBJ) moc_*.cpp

####### Link

$(GUIEXE):  $(GUIOBJ) 
	$(LINK) $(LFLAGS) -o $(GUIEXE) $(GUIOBJ) $(LIBS) $(ETHOBJ)
	-rm ../bin/$(@:.exe=)
	-ln -s `pwd`/$@ ../bin/$(@:.exe=)

%.exe: %.o $(ETHOBJ)
	$(LINK) $(LFLAGS) -o $@ $(@:.exe=.o) $(ETHOBJ)
	-rm ../bin/$(@:.exe=)
	-ln -s `pwd`/$*.exe ../bin/$(@:.exe=)

####### Compile GUI

RadTestGUI.o: RadTestGUI.cpp \
		../include/RadTestGUI.h \
		../include/RadTestWorker.h 
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)

RadTestWorker.o: RadTestWorker.cpp \
		../include/RadTestWorker.h \
		../include/RadTestThread.h \
		$(ETHOBJ)
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)

RadTestThread.o: RadTestThread.cpp \
		../include/RadTestThread.h \
		$(ETHOBJ)
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)

QProgressIndicator.o: QProgressIndicator.cpp \
		../include/QProgressIndicator.h
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)


moc_RadTestGUI.o: moc_RadTestGUI.cpp 
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)

moc_RadTestThread.o: moc_RadTestThread.cpp 
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)

moc_RadTestWorker.o: moc_RadTestWorker.cpp 
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)

moc_QProgressIndicator.o: moc_QProgressIndicator.cpp
	$(CXX) -c $(CXXFLAGS) $(INCPATH) -o $@ $(@:.o=.cpp)


# Generate moc_*.cpp files (any header with Q_OBJECT)

moc_RadTestGUI.cpp: ../include/RadTestGUI.h
	$(MOC) $(DEFINES) $(INCPATH) $< -o $@

moc_RadTestThread.cpp: ../include/RadTestThread.h
	$(MOC) $(DEFINES) $(INCPATH) $< -o $@

moc_RadTestWorker.cpp: ../include/RadTestWorker.h
	$(MOC) $(DEFINES) $(INCPATH) $< -o $@

moc_QProgressIndicator.cpp: ../include/QProgressIndicator.h
	$(MOC) $(DEFINES) $(INCPATH) $< -o $@

####### Implicit Compile Rules

%.o: %.cpp ../include/%.h $(ETHHEADERS)
	$(CXX) $(CXXFLAGS) $(INCPATH) -c -o $@ $*.cpp

%.o: %.cpp $(ETHHEADERS)
	$(CXX) $(CXXFLAGS) $(INCPATH) -c -o $@ $*.cpp

FORCE:


