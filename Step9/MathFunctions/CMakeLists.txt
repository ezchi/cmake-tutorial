# add the library that runs
add_library(MathFunctions MathFunctions.cxx)

# state taht anybody linking to us nees to include the current source dir
# to find MathFunctions.h, while we don't.
target_include_directories(MathFunctions
  INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
  )

# should we sue our own math functions
option(USE_MYMATH "Use tutorial provided math implelmentation" ON)

if (USE_MAMATH)
  target_compile_definitions(MathFunctions PRIVATE "USE_MYMATH")

  # first we add the executable that generate the table

  # add the command to generate the source code
  add_custom_command(
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/Table.h
    COMMAND MakeTable ${CMAKE_CURRENT_BINARY_DIR}/Table.h
    DEPENDS MakeTable
    )

  # library that just does sqrt
  add_library(SqrtLibrary STATIC
    mysqrt.cxx
    ${CMAKE_CURRENT_BINARY_DIR}/Table.h
    )

  # state taht we depend on our binary dir to find Table.h
  target_include_directories(SqrtLibrary PRIVATE
    ${CMAKE_CURRENT_BINARY_DIR}
    )

  # state that SqrtLibrary need PIC when the default is shared libraries
  set_target_properties(SqrtLibrary PROPERTIES
    POSITION_INDEPENDT_CODE ${BUILD_SHARED_LIBS}
    )

  target_link_libraries(MathFunctions PRIVATE SqrtLibrary)
endif()

# define the symbol stating we are using the declspec(dllexport) when
# building on windows
target_compile_definitions(MathFunctions PRIVATE "EXPORTING_MYMATH")

# install rules
set(installable_libs MathFunctions)
if(TARGET SqrtLibrary)
  list(APPEND installable_libs SqrtLibrary)
endif()

install(TARGETS ${installable_libs} DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include)
