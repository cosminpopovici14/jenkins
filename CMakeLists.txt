cmake_minimum_required(VERSION 3.10)
project(GTestExample)

# Adaugă GTest
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Adaugă fișierele sursă
set(SOURCE_FILES test_main.cpp)

add_executable(runTests ${SOURCE_FILES})
target_link_libraries(runTests ${GTEST_LIBRARIES} pthread)
