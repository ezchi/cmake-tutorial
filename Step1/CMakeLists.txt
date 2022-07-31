cmake_minimum_required (VERSION 3.15)

project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add configure file for version number
# The output configure file will be written into binrary directory.
configure_file(TutorialConfig.h.in TutorialConfig.h)

add_executable(Tutorial tutorial.cxx)
target_include_directories(Tutorial PUBLIC
  "${PROJECT_BINARY_DIR}"
  )
