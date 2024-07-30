cmake_minimum_required(VERSION 3.10)

# Numele proiectului
project(GTestProject)

# Setează standardul C++
set(CMAKE_CXX_STANDARD 11)

# Adaugă subdirectorul unde se află codul sursă
add_subdirectory(src)

# Include GoogleTest
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Adaugă fișierele de test
add_executable(test_main test_main.cpp)

# Leagă biblioteca GoogleTest cu executabilul de test
target_link_libraries(test_main ${GTEST_LIBRARIES} pthread)
