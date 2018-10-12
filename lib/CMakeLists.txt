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
set(GLM_TEST_ENABLE OFF CACHE BOOL "Build unit tests")

add_subdirectory(glm)
set(GLM_INCLUDE
	glm
	PARENT_SCOPE
)

### ASSIMP ###

include_directories(
	assimp-4.1.0/code/BoostWorkaround 
	assimp-4.1.0/include
)

# Compile without Boost
add_definitions( -DASSIMP_BUILD_BOOST_WORKAROUND )

set(BUILD_STATIC_LIB ON CACHE BOOL "Build unit tests")

set(ASSIMP_BUILD_ALL_IMPORTERS_BY_DEFAULT OFF CACHE BOOL "default value of all ASSIMP_BUILD_XXX_IMPORTER value")
set(ASSIMP_BUILD_OBJ_IMPORTER ON CACHE BOOL "build the OBJ importer")
set(ASSIMP_BUILD_3MF_IMPORTER ON CACHE BOOL "build the 3MF importer")
set(ASSIMP_BUILD_TESTS OFF CACHE BOOL "If the test suite for Assimp is built in addition to the library.")

add_subdirectory( assimp-4.1.0 )
