CC=g++

DEBUG ?= 1

ifeq ($(DEBUG),1)
   OPTFLAGS=-g
else
   OPTFLAGS=-O3
endif

CFLAGS=-I. -I../CppUnitLite -std=c++20 -Wall -Werror $(OPTFLAGS)

PROJDIR := $(realpath $(CURDIR)/..)
BUILDDIR := $(PROJDIR)/Output

DIRS = VectorGraphics

SOURCEDIRS = $(foreach dir, $(DIRS), $(addprefix $(PROJDIR)/, $(dir)))
TARGETDIRS = $(foreach dir, $(DIRS), $(addprefix $(BUILDDIR)/, $(dir))) ../bin
VPATH = $(SOURCEDIRS)
SOURCES = $(foreach dir, $(SOURCEDIRS), $(wildcard $(dir)/*.cpp))

OBJ := $(subst $(PROJDIR),$(BUILDDIR), $(SOURCES:.cpp=.o))

define generateRules
$(1)/%.o: %.cpp
	$(CXX) -c -o $$@ $$< $$(CFLAGS)
endef


$(foreach targetdir, $(TARGETDIRS), $(eval $(call generateRules, $(targetdir))))

directories:
	mkdir -p $(TARGETDIRS)

libVectorGraphics.a: $(OBJ)
	ar rcs libVectorGraphics.a $(OBJ)
	ranlib libVectorGraphics.a

all: directories libVectorGraphics.a

clean:
	rm -rf $(TARGETDIRS)
	rm -rf $(BUILDDIR)
	rm -rf *.a
