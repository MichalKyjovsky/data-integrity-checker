include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})

add_executable(runBasicTests test_connection.cpp test_output_generation.cpp)

target_link_libraries(runBasicTests gtest gtest_main)
target_link_libraries(runBasicTests src)