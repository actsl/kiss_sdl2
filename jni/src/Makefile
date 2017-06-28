CXXFLAGS = -Wall -I.
UNAME    = $(shell uname -s)

SDL_SRC = playmus.c
SDL_LIB = -lpthread -lSDL2 -lSDL2_ttf -lSDL2_image -lSDL2_mixer -lc++_shared

all: clean project1

project1:
	$(CXX) $(CXXFLAGS) `sdl2-config --cflags` -o project1 $(SDL_SRC) $(SDL_LIB)

clean:
	rm -rf sdl *.dSYM

