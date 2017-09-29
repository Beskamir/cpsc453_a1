cmake_minimum_required(VERSION 3.7)
project(Assignment1)

set(PROJECT_NAME Assignment1) #Macro the project name
set(CMAKE_CXX_STANDARD 11)


#Indicate that OpenCL is needed
find_package(OpenGL REQUIRED)
#include_directories(${OPENGL_INCLUDE_DIR})

set(SOURCE_FILES
        src/main.cpp src/main.h src/boilerplate.h)


#Gets glfw
option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
add_subdirectory(deps/glfw)

#GLEW libraries
set(GLEW_DIR "deps/glew")
include_directories(${GLEW_DIR}/include)
add_definitions(-DGLEW_STATIC)
link_directories(${GLEW_DIR}/lib)

#Create the executable using the sourcefiles
add_executable(${PROJECT_NAME} ${SOURCE_FILES})

#Link the libraries
target_link_libraries(${PROJECT_NAME} glfw glew32s ${OPENGL_LIBRARY})

#SET(CMAKE_CXX_FLAGS "-std=c++1y -lglfw -lGL -lOpenGL -lGLEW -pthread -lfreetype")

set_target_properties(${PROJECT_NAME} PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}")