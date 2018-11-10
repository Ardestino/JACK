cmake_minimum_required(VERSION 3.2)
project(compiler)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -O3")
set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR})
set(SRC ${PROJECT_SOURCE_DIR}/src)

# LLVM Libraries
# https://llvm.org/docs/CMake.html#embedding-llvm-in-your-project
find_package(LLVM REQUIRED CONFIG)
message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")
include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})
# Find the libraries that correspond to the LLVM components
llvm_map_components_to_libnames(llvm_libs support core irreader)
#

add_executable(${CMAKE_PROJECT_NAME} ${SRC}/main.cpp)

target_link_libraries(${CMAKE_PROJECT_NAME} ${llvm_libs})

install(TARGETS ${CMAKE_PROJECT_NAME} DESTINATION ${PROJECT_SOURCE_DIR}/bin)
