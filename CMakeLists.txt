cmake_minimum_required(VERSION "3.19.2")
project("LifeSim")
add_executable("LifeSim"
	"main.cpp" "test.cpp"
	"src/rendering/imgui_impl_glfw.cpp"
	"src/rendering/imgui_impl_glfw.h"
	"src/rendering/imgui_impl_opengl3.cpp"
	"src/rendering/imgui_impl_opengl3.h"
	"src/rendering/imgui_impl_opengl3_loader.h"
)

find_package(OpenGL REQUIRED)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)
set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/vendor/glfw")
include_directories("${CMAKE_CURRENT_SOURCE_DIR}/vendor/glfw/include")

set(IMGUI_PATH "${CMAKE_CURRENT_SOURCE_DIR}/vendor/imgui")
    list(APPEND sources
        ${IMGUI_PATH}/imgui.cpp
        ${IMGUI_PATH}/imgui_stdlib.cpp
        ${IMGUI_PATH}/imgui_draw.cpp
        ${IMGUI_PATH}/imgui_tables.cpp
        ${IMGUI_PATH}/imgui_widgets.cpp
        ${IMGUI_PATH}/imgui_impl_glfw.cpp
        ${IMGUI_PATH}/imgui_impl_opengl3.cpp
        ${IMGUI_PATH}/imgui_demo.cpp
    )

target_include_directories("LifeSim" PRIVATE 
    "${CMAKE_CURRENT_SOURCE_DIR}/vendor/glfw/include"
    "${IMGUI_PATH}"
)
target_link_libraries("LifeSim" PRIVATE OpenGL::GL glfw ImGui)