cmake_minimum_required(VERSION 3.15)

# set the project name and version
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

option(USE_MYMATH "Use tutorial provided math implementation" ON)

if (USE_MYMATH)
  add_subdirectory(MathFunctions)
  list(APPEND EXTRA_LIBS MathFunctions)
endif()

# add the executable
add_executable(Tutorial tutorial.cxx)

target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

# Configure a header file to pass the version number to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# The configure file will be written into the binary tree "${PROJECT_BINARY_DIR}", add it to target_include_directies
target_include_directories(Tutorial PUBLIC
  "${PROJECT_BINARY_DIR}"
  )
