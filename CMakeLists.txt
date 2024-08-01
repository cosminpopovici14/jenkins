cmake_minimum_required(VERSION 3.10)

project(MyProject)

# Include GoogleTest
add_subdirectory(googletest)

enable_testing()

# Add test executable
add_executable(gtest_main test_main.cpp)  # Asigură-te că `test_main.cpp` este fișierul tău de test

# Link test executable with GoogleTest
target_link_libraries(gtest_main gtest gmock gtest_main)
add_test(NAME my_test COMMAND gtest_main)
