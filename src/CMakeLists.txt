cmake_minimum_required(VERSION 3.17)
project(data-integrity-checker)

set(CMAKE_CXX_STANDARD 20)

add_library(data-integrity-checker configuration.hpp configuration.cpp)