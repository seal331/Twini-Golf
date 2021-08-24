cmake_minimum_required(VERSION 3.10)

project(Twini-Golf VERSION 1.1)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

configure_file(config.h.in config.h)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif(NOT CMAKE_BUILD_TYPE)

add_executable(twini_golf src/ball.cpp src/entity.cpp src/hole.cpp src/main.cpp src/renderwindow.cpp src/tile.cpp)

INCLUDE (FindPkgConfig)

IF (NOT PKG_CONFIG_FOUND)
        MESSAGE (FATAL_ERROR "pkg-config not found...")
ENDIF (NOT PKG_CONFIG_FOUND)

PKG_CHECK_MODULES(SDL2 REQUIRED IMPORTED_TARGET sdl2)
PKG_CHECK_MODULES(SDL2IMAGE REQUIRED IMPORTED_TARGET SDL2_image>=2.0.0)
PKG_CHECK_MODULES(SDL2TTF REQUIRED IMPORTED_TARGET SDL2_ttf>=2.0.0)
PKG_CHECK_MODULES(SDL2MIXER REQUIRED IMPORTED_TARGET SDL2_mixer>=2.0.0)

target_link_libraries(twini_golf PUBLIC PkgConfig::SDL2 PkgConfig::SDL2IMAGE PkgConfig::SDL2TTF PkgConfig::SDL2MIXER)

target_include_directories(twini_golf PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )

install(TARGETS twini_golf DESTINATION bin)
install(DIRECTORY res DESTINATION share/twinigolf)
