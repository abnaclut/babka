#external/glad/CMakeLists.txt
cmake_minimum_required(VERSION 3.13 FATAL_ERROR)
project(Glad)

add_library(glad STATIC include/glad/glad.h src/glad.c)
target_include_directories(glad PUBLIC include/) 
