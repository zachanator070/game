if(MSVC AND NOT "${MSVC_VERSION}" LESS 1400)
	add_definitions( "/MP" )
endif()

find_package(OpenGL REQUIRED)

add_definitions(
	-DTW_STATIC
	-DTW_NO_LIB_PRAGMA
	-DTW_NO_DIRECT3D
	-DGLEW_STATIC
	-D_CRT_SECURE_NO_WARNINGS
)

### GLFW ###

add_subdirectory (glfw-3.2.1)

include_directories(
	glfw-3.2.1/include
	glew-2.1.0/include
)

### GLEW ###

set(GLEW_SOURCE
	glew-2.1.0/src/glew.c
)

set(GLEW_HEADERS
)


add_library( glew STATIC
	${GLEW_SOURCE}
)

target_link_libraries(glew
	${OPENGL_LIBRARY}
)

### GLM ###
add_subdirectory(glm)
set(GLM_INCLUDE
	glm
	PARENT_SCOPE
)


### ASSIMP ###
# AssImp already has a CMakeLists.txt so let's use these

# Compile built-in, modified version of Zlib
#include(CheckIncludeFile)
#include(CheckTypeSize)
#include(CheckFunctionExists)

#set(ASSIMP_INCLUDE
#	assimp-4.1.0
#	PARENT_SCOPE
#)

#include_directories(
#	${ASSIMP_INCLUDE}/
#)

# Compile without Boost
include_directories(
	assimp-4.1.0/code/BoostWorkaround 
	assimp-4.1.0/include
)
add_definitions( -DASSIMP_BUILD_BOOST_WORKAROUND )

# Compile AssImp
# set(Assimp_DIR ${CMAKE_CURRENT_SOURCE_DIR}/lib/assimp-4.1.0)
# set(ASSIMP_LIB_INSTALL_DIR ${Assimp_DIR} CACHE string "location of assimp" FORCE)

# set(LIBASSIMP_COMPONENT libassimp3.0-r1270-OGLtuts)
# set(ZLIB_LIBRARIES zlib)
# set(BUILD_STATIC_LIB ON)
# set(ZLIB_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/zlib)

add_subdirectory( assimp-4.1.0/contrib/zlib )