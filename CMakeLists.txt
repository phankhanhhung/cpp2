cmake_minimum_required(VERSION 3.0.0)
project(cpp2 VERSION 0.1.0 LANGUAGES C CXX)

#include(CTest)
#enable_testing()


# Set C++ version
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find all source files for Module1
file(GLOB SORT_SOURCES "sort/*.cpp")
file(GLOB SORT_HEADERS "{SOURCE_DIR}/sort/*.h")


# Find all source files for MainApp
file(GLOB MAINAPP_SOURCES "*.cpp")
file(GLOB MAINAPP_HEADERS "*.h")
file(GLOB BASE_HEADERS "base/*.h")



# Create shared library for Module1
add_library(sort SHARED ${SORT_SOURCES})

# Set include directories for SORT
target_include_directories(sort PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/sort" "${CMAKE_CURRENT_SOURCE_DIR}/base")

# Set the output directory for the library
set_target_properties(sort PROPERTIES LIBRARY_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/bin")

# Create the main executable
add_executable(MainApp ${MAINAPP_SOURCES})

# Set include directories for MainApp
target_include_directories(MainApp PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/sort" "${CMAKE_CURRENT_SOURCE_DIR}/base")

# Link MainApp with SORT
target_link_libraries(MainApp sort)

# Set the output directory for the executable
set_target_properties(MainApp PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/bin")
