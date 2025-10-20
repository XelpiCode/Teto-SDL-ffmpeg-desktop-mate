cmake_minimum_required(VERSION 3.5)

set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
#set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Release>:Release>")

project(Teto_SFML_ffmpeg_desktop_mate)
set(CMAKE_CXX_STANDARD 23)

add_subdirectory("thirdparty/SFML")

file(GLOB_RECURSE MY_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
add_executable(Teto_SFML_ffmpeg_desktop_mate "${MY_SOURCES}")

target_link_libraries(Teto_SFML_ffmpeg_desktop_mate PRIVATE
        SFML::Graphics
        SFML::Window
        SFML::System
)

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    target_compile_definitions(Teto_SFML_ffmpeg_desktop_mate PUBLIC RESOURCES_PATH="./resources/")
else()
    # For IDE development
    target_compile_definitions(Teto_SFML_ffmpeg_desktop_mate PUBLIC RESOURCES_PATH="${CMAKE_CURRENT_SOURCE_DIR}/resources/")
endif()
