cmake_minimum_required(VERSION 3.28)
project(GameProject)

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE INTERNAL "")

# Generate compile_commands.json in source root for clangd
if(NOT CMAKE_BUILD_TYPE EQUAL "Debug")
    if(EXISTS "${CMAKE_BINARY_DIR}/compile_commands.json")
        file(COPY "${CMAKE_BINARY_DIR}/compile_commands.json" 
             DESTINATION "${CMAKE_SOURCE_DIR}")
    endif()
endif()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

include(FetchContent)

FetchContent_Declare(
    raylib
    GIT_REPOSITORY https://github.com/raysan5/raylib.git
    GIT_TAG 5.0
)

FetchContent_MakeAvailable(raylib)

include_directories(${CMAKE_SOURCE_DIR}/include)

add_executable(game 
    src/main.cpp
)

target_link_libraries(game PRIVATE raylib)

if(UNIX AND NOT APPLE)
    target_link_libraries(game PRIVATE pthread)
endif()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

add_custom_command(TARGET game POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_BINARY_DIR}/compile_commands.json
    ${CMAKE_SOURCE_DIR}/compile_commands.json
    COMMENT "Copying compile_commands.json for clangd"
)
