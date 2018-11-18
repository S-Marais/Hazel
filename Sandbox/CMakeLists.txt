cmake_minimum_required(VERSION 3.8)
project(Sandbox)

set(HZ_DEFINITIONS
        ${HZ_DEFINITIONS}
)

add_executable(Sandbox "")

set_target_properties(Sandbox PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

target_sources(Sandbox
        PRIVATE
        "${CMAKE_CURRENT_LIST_DIR}/src/SandboxApp.cpp"
)

target_compile_definitions(Sandbox PRIVATE ${HZ_DEFINITIONS})
target_link_libraries(Sandbox LINK_PUBLIC Hazel)
