cmake_minimum_required(VERSION 3.24)
project(byte-view)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(byte-view INTERFACE) 
target_include_directories(byte-view 
	INTERFACE
		${CMAKE_SOURCE_DIr}/include
)

include(FetchContent)

FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/refs/tags/v1.14.0.zip
)

FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(bv-tests
	tests/bv-tests.cpp
)
target_link_libraries(bv-tests 
	PRIVATE
       		byte-view
		GTest::gtest
		GTest::gtest_main	
)

add_test(NAME bv-tests COMMAND bv-tests) 
