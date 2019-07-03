cmake_minimum_required(VERSION 3.0)

set(MY_TARGET opengl)
set(MY_COPY_TARGET opengl-copy-binaries)

add_library(${MY_TARGET} SHARED IMPORTED GLOBAL)

set(OPENGL_COPY_BINARIES_PATH "${CMAKE_BINARY_DIR}" CACHE STRING "")
add_custom_target(${MY_COPY_TARGET}
	COMMAND ${CMAKE_COMMAND} -E copy_directory "${PROJECT_SOURCE_DIR}/binaries" "${OPENGL_COPY_BINARIES_PATH}")
add_dependencies(${MY_TARGET} ${MY_COPY_TARGET})

set_target_properties(${MY_TARGET} PROPERTIES INTERFACE_INCLUDE_DIRECTORIES "${PROJECT_SOURCE_DIR}/include")
set_target_properties(${MY_TARGET} PROPERTIES IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/binaries/freeglut.dll")
set_target_properties(${MY_TARGET} PROPERTIES IMPORTED_IMPLIB "${PROJECT_SOURCE_DIR}/binaries/freeglut.lib")
