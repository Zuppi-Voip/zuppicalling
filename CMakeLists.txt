cmake_minimum_required(VERSION 3.10)

# Set the project name
project(ZuppiCalling)

# Collect all .cpp files in the current directory
file(GLOB_RECURSE SOURCES
    ${PROJECT_SOURCE_DIR}/*.cpp
)

# Add the executable
add_executable(ZuppiCalling ${SOURCES})

# Include directories
include_directories(
    ${PROJECT_SOURCE_DIR}
)

# Define preprocessor macros
add_definitions(-D_AFXDLL)

# Link required libraries
target_link_libraries(ZuppiCalling
    ws2_32
    winmm
    mfc
)
