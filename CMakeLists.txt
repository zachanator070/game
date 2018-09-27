# CMake entry point
cmake_minimum_required (VERSION 3.0)
project (game)

find_package(OpenGL REQUIRED)

# Compile external dependencies 
add_subdirectory (external)

include_directories(
	external/glfw-3.2.1/include/
	external/glew-2.1.0/include/
)

set(ALL_LIBS
	${OPENGL_LIBRARY}
	glfw
	GLEW_1130
)

add_definitions(
	-DTW_STATIC
	-DTW_NO_LIB_PRAGMA
	-DTW_NO_DIRECT3D
	-DGLEW_STATIC
	-D_CRT_SECURE_NO_WARNINGS
)

add_executable(game 
	game/game.cpp
	common/shader.cpp
	common/shader.hpp
)
target_link_libraries(game
	${ALL_LIBS}
)
