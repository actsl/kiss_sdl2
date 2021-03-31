cmake_minimum_required(VERSION 3.19)

project(SDL2_kiss LANGUAGES C CXX)

include (GNUInstallDirs)
include (FindPkgConfig)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

################################################################################
# Dependencies
################################################################################

find_package(SDL2 REQUIRED)
pkg_search_module(SDL2_MIXER REQUIRED SDL2_mixer)
pkg_search_module(SDL2_TTF REQUIRED SDL2_ttf)
pkg_search_module(SDL2_IMAGE REQUIRED SDL2_image)

################################################################################
# kiss_sdl2
################################################################################
set(SOURCE_FILES
    "include/SDL2/SDL_kiss.h"
    "src/kiss_general.c"
    "src/kiss_draw.c"
    "src/kiss_posix.c"
    "src/kiss_widgets.c"
)
add_library(${PROJECT_NAME} ${SOURCE_FILES})
add_definitions( -DIMAGE_DIR="${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME}/" )
target_include_directories(${PROJECT_NAME} PUBLIC
     "${CMAKE_SOURCE_DIR}/include"
)
target_compile_options(${PROJECT_NAME} PUBLIC ${SDL2_MIXER_CFLAGS}
	${SDL2_TTF_CFLAGS} ${SDL2_IMAGE_CFLAGS})
target_link_libraries(${PROJECT_NAME} PUBLIC ${SDL2_MIXER_LIBRARIES}
	${SDL2_TTF_LIBRARIES} ${SDL2_IMAGE_LIBRARIES})

################################################################################
# kiss_example1
################################################################################
add_executable(kiss_example1 examples/kiss_example1.c)

target_include_directories(kiss_example1 PUBLIC
     "${CMAKE_SOURCE_DIR}/include"
)

target_link_libraries(kiss_example1 PUBLIC ${PROJECT_NAME}
)

################################################################################
# kiss_example2
################################################################################
add_executable(kiss_example2 examples/kiss_example2.c)

target_include_directories(kiss_example2 PUBLIC
     "${CMAKE_SOURCE_DIR}/include"
)

target_link_libraries(kiss_example2 PUBLIC ${PROJECT_NAME}
)
install(
    TARGETS ${PROJECT_NAME}
)

set(ROOT_NAMESPACE kiss_sdl2)
