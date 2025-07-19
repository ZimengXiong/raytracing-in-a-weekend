cmake_minimum_required(VERSION 3.10)

# Correct usage of project with VERSION and LANGUAGES
project(Raytracing\ in\ a\ Weekend VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories(include)

# Grab all .cpp files in src/
file(GLOB SOURCES "src/*.cpp")

# Loop over each file and create a separate executable
foreach(SRC ${SOURCES})
    get_filename_component(FILENAME ${SRC} NAME_WE)
    add_executable(${FILENAME} ${SRC})

    if (MSVC)
        target_compile_options(${FILENAME} PRIVATE /W4)
    else()
        target_compile_options(${FILENAME} PRIVATE -Wall -Wextra -pedantic)
    endif()
endforeach()
