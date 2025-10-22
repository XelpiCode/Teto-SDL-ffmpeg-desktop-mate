cmake_minimum_required(VERSION 3.5)

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Release>:Release>")
else()
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()
set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build all libs static" FORCE)

project(Teto_SFML_ffmpeg_desktop_mate)
set(CMAKE_CXX_STANDARD 23)

set(SDL_SHARED OFF CACHE BOOL "Build SDL shared" FORCE)
set(SDL_STATIC ON  CACHE BOOL "Build SDL static" FORCE)

add_subdirectory("thirdparty/SDL" EXCLUDE_FROM_ALL)

file(GLOB_RECURSE MY_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
add_executable(Teto_SFML_ffmpeg_desktop_mate "${MY_SOURCES}")

target_link_libraries(Teto_SFML_ffmpeg_desktop_mate PRIVATE
    SDL3::SDL3-static
)

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    target_compile_definitions(Teto_SFML_ffmpeg_desktop_mate PUBLIC RESOURCES_PATH="./resources/")
else()
    # For IDE development
    target_compile_definitions(Teto_SFML_ffmpeg_desktop_mate PUBLIC RESOURCES_PATH="${CMAKE_CURRENT_SOURCE_DIR}/resources/")
endif()
