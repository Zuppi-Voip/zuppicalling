cmake_minimum_required(VERSION 3.10)

# Set the project name
project(ZuppiCalling)

# Collect all source files
file(GLOB_RECURSE SOURCES
    ${PROJECT_SOURCE_DIR}/*.cpp
    ${PROJECT_SOURCE_DIR}/lib/*.cpp
)

# Add executable
add_executable(ZuppiCalling ${SOURCES})

# Include directories
include_directories(
    ${PROJECT_SOURCE_DIR}/lib
    ${PROJECT_SOURCE_DIR}/include
    ${PROJECT_SOURCE_DIR}
)

# Define macros
add_definitions(-D_AFXDLL -D_CRT_SECURE_NO_WARNINGS)

# Link libraries
target_link_libraries(ZuppiCalling
    ws2_32
    winmm
    mfc
    pjsua
    pjlib
)
