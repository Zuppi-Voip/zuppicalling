cmake_minimum_required(VERSION 3.10)

# Set the project name
project(ZuppiCalling)

# Add executable target
add_executable(ZuppiCalling
    src/main.cpp  # Replace with actual source files
    src/other_file.cpp  # Add all relevant .cpp files
)

# Include directories
include_directories(
    ${PROJECT_SOURCE_DIR}/include
)

# Link any required libraries
target_link_libraries(ZuppiCalling
    ws2_32
    winmm
    # Add other required libraries here
)
