# CMake entry point
cmake_minimum_required (VERSION 3.0)
project (game)

find_package(OpenGL REQUIRED)

set(LIBS_DIR
	lib
)

# Compile external dependencies 
add_subdirectory (${LIBS_DIR})

include_directories(
	${LIBS_DIR}/${GLFW_INCLUDE}
	${LIBS_DIR}/${GLEW_INCLUDE}
)

set(ALL_LIBS
	${OPENGL_LIBRARY}
	glfw
	glew
)

add_definitions(
	-DTW_STATIC
	-DTW_NO_LIB_PRAGMA
	-DTW_NO_DIRECT3D
	-DGLEW_STATIC
	-D_CRT_SECURE_NO_WARNINGS
)

# compile main executable
add_executable(game 
	game/game.cpp
	common/shader.cpp
	common/shader.hpp
)
target_link_libraries(game
	${ALL_LIBS}
)
