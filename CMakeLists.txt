# CMakeLists.txt

cmake_minimum_required(VERSION 3.4)

project(simpleFA VERSION 1.0
                      DESCRIPTION "Multimodule project")

include_directories( ./lib ./src)
add_subdirectory(FA_rulez/FA_r1)
if (MSVC)
    # warning level 4 and all warnings as errors
    add_compile_options(/W4 /WX)
else()
    # lots of warnings and all warnings as errors
    add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()

############################################################################
# compile with runtime shared lib
############################################################################
add_executable(simpleFA src/main.cpp)
if (UNIX)
    target_link_libraries(simpleFA dl)
    target_compile_options(simpleFA PRIVATE -rdynamic)
endif()
