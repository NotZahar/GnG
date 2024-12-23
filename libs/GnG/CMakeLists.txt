cmake_minimum_required(VERSION 3.28)

project("GnG" VERSION 0.0.1)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(${PROJECT_NAME} STATIC)

target_sources(${PROJECT_NAME}
    PRIVATE
        src/test.cc
)

target_include_directories(${PROJECT_NAME}
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/src
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

set(PUBLIC_HEADERS
    include/test.hh
)

set_target_properties(${PROJECT_NAME} 
    PROPERTIES PUBLIC_HEADER "${PUBLIC_HEADERS}")

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

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(Installing)
