cmake_minimum_required(VERSION 3.7)
project(Sandbox)

set(HZ_DEFINITIONS
        ${HZ_DEFINITIONS}
)

set(SB_HEADER_FILES
)

set(SB_SOURCE_FILES
        src/SandboxApp.cpp
)

add_executable(Sandbox ${SB_HEADER_FILES} ${SB_SOURCE_FILES})
set_target_properties(Sandbox PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
target_compile_definitions(Sandbox PRIVATE ${HZ_DEFINITIONS})
target_link_libraries(Sandbox LINK_PUBLIC Hazel)
