# Available make targets: `make`, `make clean`, `make run`
#
# To compile on OSX make sure you have the following headers
# - Eigen in /usr/local/include/Eigen
# - glm in /usr/local/include/GLFW
# - glew headers in /usr/local/include/GL
# - glfw headers in /usr/local/include/GLFW
#
# Eigen and glm are header-only libraries, 
# you can just download them
#
# For GLEW you need to download the source, make && sudo make install
# To install GLFW you probably need cmake and then make && make install

CC = g++
CFLAGS := -std=c++11

# OSX
ifeq ("$(shell uname)", "Darwin")
	LFLAGS := -lglfw -framework Cocoa -framework CoreVideo -framework OpenGL -framework IOKit -lGLEW
# Linux - warning: untested and probably broken
else
	LFLAGS := -lGL -lfreeglut -lGLEW 
endif

L_DIR := -L/usr/local/lib
INC_DIR := -I/usr/local/include -I./include/imgui

BIN = Cartel
SRC := $(wildcard *.cpp) $(wildcard include/imgui/*.cpp)
OBJ = $(SRC:%.cpp=build/%.o)

default: build
build: $(BIN) 

$(BIN): build/main.o $(OBJ)
	$(CC) $(L_DIR) $(LFLAGS) -o $@ $^

build/%.o: %.cpp
	@ mkdir -p $(@D)
	$(CC) $(INC_DIR) $(CFLAGS) -c $< -o $@

clean:
	rm -rf *~ $(OBJ) $(BIN) build
	
run: build execute
	
execute:
	./$(BIN)
