CXX       = mipsel-linux-g++
C         = mipsel-linux-gcc
LD        = mipsel-linux-ld

PROJECT_NAME = digger

SRC_PATH = ../..
OBJ_BASE = Release
DIST_PATH = $(OBJ_BASE)
OBJ_PATH = $(OBJ_BASE)
RES_PATH = res

SRCFOLDERS = .
LIBS      = -lSDL -lz

STD_OPTS  = -O3 -Wall -c -fmessage-length=0 -DNDEBUG -D_SDL -DLINUX `sdl-config --cflags` 
CPP_OPTS  = $(STD_OPTS) -fno-rtti -fno-threadsafe-statics
C_OPTS    = $(STD_OPTS)
LD_OPTS   = `sdl-config --libs` -lz

CXXSRCS = $(foreach dir, $(SRCFOLDERS), $(wildcard $(SRC_PATH)/$(dir)/*.cpp))
CSRCS = $(foreach dir, $(SRCFOLDERS), $(wildcard $(SRC_PATH)/$(dir)/*.c))

CXX_OBJS = $(patsubst $(SRC_PATH)/%.cpp,$(OBJ_PATH)/%.o,$(CXXSRCS))
CXX_DEPS = $(patsubst $(SRC_PATH)/%.cpp,$(OBJ_PATH)/%.d,$(CXXSRCS))
C_OBJS = $(patsubst $(SRC_PATH)/%.c,$(OBJ_PATH)/%.o,$(CSRCS))
C_DEPS = $(patsubst $(SRC_PATH)/%.c,$(OBJ_PATH)/%.d,$(CSRCS))

BIN_TARGET = $(DIST_PATH)/$(PROJECT_NAME)

build: mkdirs $(BIN_TARGET)

mkdirs:
	mkdir -p $(DIST_PATH)
	mkdir -p $(foreach dir, $(SRCFOLDERS), $(OBJ_PATH)/$(dir))

$(CXX_OBJS): $(OBJ_PATH)/%.o : $(SRC_PATH)/%.cpp
	$(CXX) $(CPP_OPTS) -o $@ $<

$(C_OBJS): $(OBJ_PATH)/%.o : $(SRC_PATH)/%.c
	$(C) $(C_OPTS) -o $@ $<

$(BIN_TARGET): $(CXX_OBJS) $(C_OBJS)
	$(C) $(CXX_OBJS) $(C_OBJS) $(LD_OPTS) -o $(BIN_TARGET)

clean:
	rm -rf $(OBJ_BASE)
	rm -rf $(DIST_PATH)

.PHONY: mkdirs clean build
