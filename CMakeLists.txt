cmake_minimum_required(VERSION 3.14)
project(video-app CXX)
set(CMAKE_CXX_STANDARD 14)

add_subdirectory(lib/glfw)
add_subdirectory(lib/FFmpeg)

add_definitions(-DGL_SILENCE_DEPRECATION)

if(APPLE)
    list(APPEND EXTRA_LIBS
        "-framework OpenGL"
    )
elseif(WIN32)
    list(APPEND EXTRA_LIBS
        "-lglu32 -lopengl32"
    )
    set(CMAKE_EXE_LINKER_FLAGS "-std=gnu99 -static -static-libgcc -static-libstdc++ -mwindows")
else()
    list(APPEND EXTRA_LIBS
        "-lGL -lGLU -LX11"
    )
endif()

add_executable(video-app src/main.cpp)
target_link_libraries(video-app FFmpeg glfw ${EXTRA_LIBS})
