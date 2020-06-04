cmake_minimum_required(VERSION 3.12)
project ("Tmpl8_2018-01")

# FindFreeImage.cmake and FindSDL2.cmake are not part of cmake by default, use modified third-party scripts:
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})

set (GLEW_INCLUDE_DIR  "${CMAKE_CURRENT_SOURCE_DIR}/lib/glew-2.1.0/include")
set (GLEW_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/glew-2.1.0/lib/x64/glew32.lib")

set (SDL2_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/SDL2-2.0.9/lib/x64/SDL2.lib")
set (SDL2_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/lib/SDL2-2.0.9/include")
set (SDL2_SDLMAIN_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/SDL2-2.0.9/lib/x64/SDL2main.lib")

set (FREEIMAGE_LIBRARY "${CMAKE_CURRENT_SOURCE_DIR}/lib/FreeImage/lib64/FreeImage.lib")
set (FREEIMAGE_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/lib/FreeImage/include")

set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(SDL2 REQUIRED)
find_package(FreeImage REQUIRED)

# Compile all "*.cpp" files in the root directory:
file(GLOB SOURCES "*.cpp")
add_executable(${PROJECT_NAME} ${SOURCES})

message("CMAKE_CURRENT_SOURCE_DIR = ")

#target_include_directories(${PROJECT_NAME} PUBLIC "./")

#if (MSVC)
#   set_target_properties(${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "precomp.h")
#   set_source_files_properties(${SOURCES} PROPERTIES COMPILE_FLAGS "precomp.h")
#endif(MSVC)

#target_precompile_headers(${PROJECT_NAME} PUBLIC precomp.h)

target_link_libraries(${PROJECT_NAME} PRIVATE OpenGL::GL)
target_link_libraries(${PROJECT_NAME} PRIVATE GLEW::GLEW)
target_link_libraries(${PROJECT_NAME} PRIVATE SDL2::SDL2)
target_link_libraries(${PROJECT_NAME} PRIVATE FreeImage::freeimage)

# AVX2 support (Intel Haswell and higher)
#set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-mavx2")

set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 14 # Require C++ 14
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)

# Uncomment this line to see warnings. Useful to
# find those pesky mistakes/typos.
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")
