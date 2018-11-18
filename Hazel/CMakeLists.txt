cmake_minimum_required(VERSION 3.8)
project(Hazel)

set(CMAKE_CXX_STANDARD 17)

add_library(spdlog INTERFACE IMPORTED)
set_target_properties(spdlog PROPERTIES INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_SOURCE_DIR}/Hazel/libs/spdlog/include)

add_library(Hazel SHARED "")
set_target_properties(Hazel PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

target_sources(Hazel
        PUBLIC
        "${CMAKE_CURRENT_LIST_DIR}/include/Hazel.h"
        "${CMAKE_CURRENT_LIST_DIR}/include/Hazel/Application.h"
        "${CMAKE_CURRENT_LIST_DIR}/include/Hazel/Core.h"
        "${CMAKE_CURRENT_LIST_DIR}/include/Hazel/EntryPoint.h"
        "${CMAKE_CURRENT_LIST_DIR}/include/Hazel/Log.h"
        PRIVATE
        src/Hazel/Application.cpp
        src/Hazel/Log.cpp
)

set(HZ_DEFINITIONS
        -DHZ_BUILD_SHARED
        ${HZ_DEFINITIONS}
)
if (CMAKE_DUILD_TYPE STREQUAL "Debug")
    set(HZ_DEFINITIONS
            -DHZ_DEBUG
            ${HZ_DEFINITIONS}
    )
endif()

target_include_directories(Hazel PUBLIC include include/Hazel)
target_compile_definitions(Hazel PRIVATE ${HZ_DEFINITIONS})
target_link_libraries(Hazel spdlog)
