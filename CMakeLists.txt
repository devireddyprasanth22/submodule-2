cmake_minimum_required(VERSION 3.10)
project(submodule-2)

enable_testing()

# Create a library that can be linked against
add_library(submodule2_lib submodule2.c)

# Create the executable with a different name
add_executable(submodule2 submodule2.c)

# Add Google Test
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Compile test executable
add_executable(test-submodule2 test-submodule2.cpp)
target_link_libraries(test-submodule2 GTest::GTest GTest::Main pthread submodule2_lib)

# Register test with CTest
add_test(NAME submodule2_test COMMAND test-submodule2)

# Make the library target available to parent projects
set_target_properties(submodule2_lib PROPERTIES EXPORT_NAME submodule2_lib)
