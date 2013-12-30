project(cairo)
cmake_minimum_required(VERSION 2.8)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

if (WIN32)
    set(CAIRO_LIBS gdi32 msimg32 user32 winmm)
endif()

find_package(freetype)
find_package(fontconfig)
find_package(pixman REQUIRED)
find_package(png REQUIRED)
find_package(zlib REQUIRED)

include_directories(${FREETYPE_INCLUDE_DIRS} ${PIXMAN_INCLUDE_DIR} ${PNG_INCLUDE_DIR} ${ZLIB_INCLUDE_DIR})
list(APPEND CAIRO_LIBS  ${FREETYPE_LIBRARY} ${FONTCONFIG_LIBRARY} ${PIXMAN_LIBRARY} ${PNG_LIBRARY} ${ZLIB_LIBRARY})

include(Configure_config.cmake)
include(Configure_features.cmake)
include_directories(${CMAKE_BINARY_DIR})

include_directories(src)
add_subdirectory(src)

if (CIARO_BUILD_STATIC)
     add_definition(-DCAIRO_WIN32_STATIC_BUILD=1)
endif()