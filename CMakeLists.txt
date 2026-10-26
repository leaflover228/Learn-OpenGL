cmake_minimum_required(VERSION 3.16)
project(learn-opengl LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

set(EXTERNAL_LIBS_ROOT "C:/Users/shedoesntlove/Documents/Visual Studio 18/External Libs" CACHE PATH "External libs root")

set(GLEW_ROOT "${EXTERNAL_LIBS_ROOT}/GLEW")
set(GLFW_ROOT "${EXTERNAL_LIBS_ROOT}/GLFW")

set(GLEW_INCLUDE_DIR "${GLEW_ROOT}/include")
set(GLFW_INCLUDE_DIR "${GLFW_ROOT}/include")

option(USE_STATIC_GLEW "Link GLEW statically" OFF)
option(USE_STATIC_GLFW "Link GLFW statically" OFF)

if(USE_STATIC_GLEW)
    set(GLEW_LIB "${GLEW_ROOT}/lib/Release/x64/glew32s.lib")
    set(GLEW_DEFINITIONS GLEW_STATIC)
else()
    set(GLEW_LIB "${GLEW_ROOT}/lib/Release/x64/glew32.lib")
    set(GLEW_DLL "${GLEW_ROOT}/bin/Release/x64/glew32.dll")
endif()

set(GLFW_LIB_DIR "${GLFW_ROOT}/lib-vc2026" CACHE PATH "GLFW MSVC lib folder")

if(USE_STATIC_GLFW)
    set(GLFW_LIB "${GLFW_LIB_DIR}/glfw3_mt.lib")
else()
    set(GLFW_LIB "${GLFW_LIB_DIR}/glfw3dll.lib")
    set(GLFW_DLL "${GLFW_LIB_DIR}/glfw3.dll")
endif()

add_subdirectory(lesson_1)
# add_subdirectory(lesson_2)
# add_subdirectory(lesson_3)
# add_subdirectory(lesson_4)
# add_subdirectory(lesson_5)
