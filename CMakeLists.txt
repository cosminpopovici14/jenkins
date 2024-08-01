# CMakeLists.txt

# Adăugăm submodulul GoogleTest
add_subdirectory(tests/gtest)

# Adăugăm teste
enable_testing()

# Adăugăm executabilul testelor
add_executable(test_main tests/main.cpp)

# Linkăm GoogleTest
target_link_libraries(test_main gtest gtest_main)

# Definim testele
add_test(NAME MyTests COMMAND test_main)
