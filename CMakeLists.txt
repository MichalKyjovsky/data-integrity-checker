CMAKE_MINIMUM_REQUIRED(VERSION 3.17)
project(data-integrity-checker)

set(CMAKE_CXX_STANDARD 20)

add_definitions(-std=gnu++0x)
set(SOURCE_FILES main.cpp)

add_executable(data_integrity_checker_run ${SOURCE_FILES})

include_directories(src)

add_subdirectory(src)
add_subdirectory(test)

target_link_libraries(data_integrity_checker_run data-integrity-checker)