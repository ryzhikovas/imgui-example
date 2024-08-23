cmake_minimum_required(VERSION 3.28)
project(untitled)

set(CMAKE_CXX_STANDARD 17)

include(FetchContent)

FetchContent_Declare(
        imgui
        GIT_REPOSITORY https://github.com/ocornut/imgui
        GIT_TAG v1.91.0)
FetchContent_MakeAvailable(imgui)

file(GLOB imgui_CPP ${imgui_SOURCE_DIR}/*.cpp)

add_executable(imgui_example
        main.cpp
        ${imgui_CPP}
        "${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.cpp"
        "${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp"
)

find_package(OpenGL REQUIRED)

target_include_directories(imgui_example PRIVATE ${imgui_SOURCE_DIR})

target_link_libraries(imgui_example glfw OpenGL::GL)

if (MSVC)
    target_compile_options(imgui_example PUBLIC /W4)
else ()
    target_compile_options(imgui_example PUBLIC -Wall -Wextra -Wpedantic -Wconversion -Wsign-conversion)
endif ()