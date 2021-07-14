cmake_minimum_required(VERSION 3.10)
project(cmake)

set(FILES 
    greeter.cpp
    person.cpp)

add_library(${PROJECT_NAME}-lib ${FILES})
add_executable(${PROJECT_NAME} main.cpp)
add_executable(${PROJECT_NAME}-test test/greeter.ut.cpp)
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME}-lib)
target_compile_options(${PROJECT_NAME}-lib PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)
target_compile_options(${PROJECT_NAME}-test PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)

target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)
target_compile_features(${PROJECT_NAME}-lib PRIVATE cxx_std_20)
target_compile_features(${PROJECT_NAME}-test PRIVATE cxx_std_20)

enable_testing()
add_test(NAME tests COMMAND ${PROJECT_NAME}-test)