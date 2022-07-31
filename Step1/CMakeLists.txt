cmake_minimum_required (VERSION 3.15)

project(Tutorial VERSION 1.0)

# Add configure file for version number
# The output configure file will be written into binrary directory.
configure_file(TutorialConfig.h.in TutorialConfig.h)

add_executable(Tutorial tutorial.cxx)
target_include_directories(Tutorial PUBLIC
  "${PROJECT_BINARY_DIR}"
  )
