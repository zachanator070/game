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
	${LIBS_DIR}/glew-2.1.0/include
	${LIBS_DIR}/glfw-3.2.1/include
	${LIBS_DIR}/glm
	${LIBS_DIR}/assimp-4.1.0/include
	${CMAKE_BINARY_DIR}/lib/assimp-4.1.0/include
	game
	.
	${CMAKE_BINARY_DIR}
)

set(ALL_LIBS
	${OPENGL_LIBRARY}
	glfw
	glew
	glm
	assimp
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
	game/gengine/controls.cpp
	game/gengine/controls.hpp
	game/gengine/objloader.cpp
	game/gengine/objloader.hpp
	game/gengine/shader.cpp
	game/gengine/shader.hpp
	game/gengine/texture.cpp
	game/gengine/texture.hpp
)

FILE(COPY game/suzanne.obj DESTINATION "${CMAKE_BINARY_DIR}")
FILE(COPY game/StandardShading.fragmentshader DESTINATION "${CMAKE_BINARY_DIR}")
FILE(COPY game/StandardShading.vertexshader DESTINATION "${CMAKE_BINARY_DIR}")
FILE(COPY game/uvmap.DDS DESTINATION "${CMAKE_BINARY_DIR}")

target_link_libraries(game
	${ALL_LIBS}
)
