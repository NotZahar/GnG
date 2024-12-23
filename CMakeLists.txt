cmake_minimum_required(VERSION 3.28)

set(PATCH_VERSION 1 CACHE INTERNAL "Patch version")
set(PROJECT_VESRION 0.0.${PATCH_VERSION})

project("gng" VERSION ${PROJECT_VESRION})

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(libs)

add_executable(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
    PRIVATE
        src/main.cpp
)

target_link_libraries(${PROJECT_NAME} 
    PRIVATE 
        GnG
)

if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_compile_options(
        ${PROJECT_NAME}
            PRIVATE
                -Wall
                -Wextra
                -Werror
                -pedantic
    )
else()
    target_compile_options(
        ${PROJECT_NAME}
            PRIVATE
                /Wall
                /WX
    )
endif()

add_compile_definitions("GNG_DEBUG_MODE=$<CONFIG:Debug>")
