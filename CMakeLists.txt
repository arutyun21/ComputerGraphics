# CMake entry point
cmake_minimum_required (VERSION 3.0)
project (Tutorials)

find_package(OpenGL REQUIRED)


if( CMAKE_BINARY_DIR STREQUAL CMAKE_SOURCE_DIR )
    message( FATAL_ERROR "Please select another Build Directory ! (and give it a clever name, like bin_Visual2012_64bits/)" )
endif()
if( CMAKE_SOURCE_DIR MATCHES " " )
    message( "Your Source Directory contains spaces. If you experience problems when compiling, this can be the cause." )
endif()
if( CMAKE_BINARY_DIR MATCHES " " )
    message( "Your Build Directory contains spaces. If you experience problems when compiling, this can be the cause." )
endif()



# Compile external dependencies
add_subdirectory (external)

# On Visual 2005 and above, this module can set the debug working directory
cmake_policy(SET CMP0026 OLD)
list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/external/rpavlik-cmake-modules-fe2273")
include(CreateLaunchers)
include(MSVCMultipleProcessCompile) # /MP

if(INCLUDE_DISTRIB)
    add_subdirectory(distrib)
endif(INCLUDE_DISTRIB)



include_directories(
        external/AntTweakBar-1.16/include/
        external/glfw-3.1.2/include/
        external/glm-0.9.7.1/
        external/glew-1.13.0/include/
        external/assimp-3.0.1270/include/
        external/bullet-2.81-rev2613/src/
        .
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

# Task 1
add_executable(task_01
        task_01/task_01.cpp
        common/shader.cpp
        common/shader.hpp

        task_01/SimpleFragmentShader.fragmentshader
        task_01/SimpleVertexShader.vertexshader
        )
target_link_libraries(task_01
        ${ALL_LIBS}
        )

# Xcode and Visual working directories
set_target_properties(task_01 PROPERTIES XCODE_ATTRIBUTE_CONFIGURATION_BUILD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/task_01/")
create_target_launcher(task_01 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_01/")
create_default_target_launcher(task_01 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_01/")

# Task 2
add_executable(task_02
        task_02/task_02.cpp
        common/shader.cpp
        common/shader.hpp

        task_02/VertexShader.vertexshader
        task_02/RedFragmentShader.fragmentshader
        task_02/BlueFragmentShader.fragmentshader
        )
target_link_libraries(task_02
        ${ALL_LIBS}
        )

# Xcode and Visual working directories
set_target_properties(task_02 PROPERTIES XCODE_ATTRIBUTE_CONFIGURATION_BUILD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/task_02/")
create_target_launcher(task_02 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_02/")
create_default_target_launcher(task_02 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_02/") 

# Task 3
add_executable(task_03
        task_03/task_03.cpp
        common/shader.cpp
        common/shader.hpp

        task_03/Transform.vertexshader
        task_03/RedFragmentShader.fragmentshader
        task_03/BlueFragmentShader.fragmentshader
        )
target_link_libraries(task_03
        ${ALL_LIBS}
        )

# Xcode and Visual working directories
set_target_properties(task_03 PROPERTIES XCODE_ATTRIBUTE_CONFIGURATION_BUILD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/task_03/")
create_target_launcher(task_03 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_03/")
create_default_target_launcher(task_03 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_03/")

# Task 4
add_executable(task_04
        task_04/task_04.cpp
        common/shader.cpp
        common/shader.hpp

        task_04/ColorFragmentShader.fragmentshader
        task_04/Transform.vertexshader
        )
target_link_libraries(task_04
        ${ALL_LIBS}
        )
# Xcode and Visual working directories
set_target_properties(task_04 PROPERTIES XCODE_ATTRIBUTE_CONFIGURATION_BUILD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/task_04/")
create_target_launcher(task_04 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_04/")
create_default_target_launcher(task_04 WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/task_04/") 