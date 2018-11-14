cmake_minimum_required(VERSION 3.7)
project(Hazel)

set(CMAKE_CXX_STANDARD 17)

add_library(spdlog INTERFACE IMPORTED)
set_target_properties(spdlog PROPERTIES INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_SOURCE_DIR}/Hazel/libs/spdlog/include)

set(HZ_HEADER_FILES
        include/Hazel.h
        include/Hazel/Application.h
        include/Hazel/Core.h
        include/Hazel/EntryPoint.h
        include/Hazel/Log.h
)

set(HZ_SOURCE_FILES
        src/Hazel/Application.cpp
        src/Hazel/Log.cpp
)

add_library(Hazel SHARED ${HZ_HEADER_FILES} ${HZ_SOURCE_FILES})
set_target_properties(Hazel PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
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
