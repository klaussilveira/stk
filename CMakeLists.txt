cmake_minimum_required(VERSION 3.14)
project(st)

set(CMAKE_C_STANDARD 11)
set(SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/src)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR})

find_package(X11 REQUIRED)
find_package(Freetype REQUIRED)
find_package(Fontconfig REQUIRED)

set(PROJECT_SOURCES
        ${SOURCE_DIR}/st.c
        ${SOURCE_DIR}/x.c)

set(PROJECT_INCLUDE_DIRS
        ${SOURCE_DIR}
        ${FREETYPE_INCLUDE_DIRS}
        ${X11_INCLUDE_DIR})

include_directories(${PROJECT_INCLUDE_DIRS})
add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})
target_link_libraries(${PROJECT_NAME} m util ${Fontconfig_LIBRARIES} ${X11_LIBRARIES} ${FREETYPE_LIBRARIES} ${X11_Xft_LIB})
target_compile_options(${PROJECT_NAME} PUBLIC -Wall -Wextra)

if (CMAKE_BUILD_TYPE MATCHES RELEASE)
    target_compile_options(${PROJECT_NAME} PUBLIC -O3 -ffast-math)
endif()