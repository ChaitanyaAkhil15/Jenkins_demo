cmake_minimum_required(VERSION 3.10)

project(AdditionProject)

set(CMAKE_CXX_STANDARD 14)

# Add your source files
add_executable(addition_project src/main.cpp)

# Add a custom target for clang-format
find_program(CLANG_FORMAT_EXE clang-format)
if(CLANG_FORMAT_EXE)
    file(GLOB_RECURSE ALL_SOURCE_FILES src/*.cpp src/*.h)
    add_custom_target(
        clang-format
        COMMAND ${CLANG_FORMAT_EXE}
        -i
        -style=file
        ${ALL_SOURCE_FILES}
    )
endif()

# Add a custom target for clang static analysis
find_program(CLANG_ANALYZER_EXE scan-build)
if(CLANG_ANALYZER_EXE)
    add_custom_target(
        clang-static-analysis
        COMMAND ${CLANG_ANALYZER_EXE}
        cmake --build .
    )
endif()
