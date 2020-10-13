cmake_minimum_required(VERSION 3.15)

# set the project name and version
project(Tutorial VERSION 1.0)

# add the executable
add_executable(Tutorial tutorial.cxx)

# Configure a header file to pass the version number to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# The configure file will be written into the binary tree "${PROJECT_BINARY_DIR}", add it to target_include_directies
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )
