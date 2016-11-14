cmake_minimum_required(VERSION 3.6)
set(PROJ_NAME Vukan_Test)
project(${PROJ_NAME})

#set up linux search paths
set(LIBRARY_SEARCH_PATH
        /usr/local
        /opt/local
        /usr
        /opt
        )

set(HEADER_SEARCH_PATH
        /usr/local
        /opt/local
        /usr
        #        /opt
        )

include_directories(/home/sensetime/VulkanSDK/1.0.30.0/x86_64/include)

# Find OpenGL
find_package(OpenGL)
find_package(X11)

# Find glfw header
find_path(GLFW_INCLUDE_DIR GLFW/glfw3.h ${HEADER_SEARCH_PATH})

# Find vulkan header
#find_path(VULKAN_INCLUDE_DIR Vulkan/vulkan.h ${HEADER_SEARCH_PATH})
#add_library(vulkan SHARED "vulkan")

# Find glfw library
find_library(GLFW_LIBRARIES glfw3 ${LIBRARY_SEARCH_PATH})

# Set additional libs
set( ADDITIONAL_LIBS
        #        -lGLEW
        -lGL
        -lGLU
        -lglfw3
        -lX11
        -lpthread
        -lrt
        -lXinerama
        -lXrandr
        -lXxf86vm
        -lXi
        -lXcursor
        -ldl
        )

# Include directories for this project
set(INCLUDE_PATH
        ${OPENGL_INCLUDE_DIR}
        ${GLFW_INCLUDE_DIR}
        #        ${VULKAN_INCLUDE_DIR}
        )

# Libraries needed on all platforms for this project
set(LIBRARIES
        ${OPENGL_LIBRARIES}
        ${GLFW_LIBRARIES}
        ${X11_LIBRARIES}
        ${ADDITIONAL_LIBS}
        )

# Windows and Linux need GLEW, the OpenGL Extension Wrangler
#find_path(GLEW_INCLUDE_DIR GL/glew.h
#        ${HEADER_SEARCH_PATH}
#        )

set(INCLUDE_PATH ${INCUDE_PATH}
#        ${GLEW_INCLUDE_DIR}
        )

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILES main.cpp)
# Add a target executable

link_directories(/home/sensetime/VulkanSDK/1.0.30.0/x86_64/lib)

add_executable(${PROJ_NAME}
        ${SOURCE_FILES}
        )

# Libraries to be linked
target_link_libraries(${PROJ_NAME}
        ${LIBRARIES}
        "vulkan"
        )