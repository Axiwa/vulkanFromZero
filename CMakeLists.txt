cmake_minimum_required(VERSION 3.20)
project(zeroVulkan LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Vulkan REQUIRED)
find_package(SDL3 REQUIRED CONFIG PATHS "$ENV{VULKAN_SDK}")

add_executable(main main.cpp)

target_link_libraries(main PRIVATE Vulkan::Vulkan SDL3::SDL3)

target_compile_definitions(main PRIVATE 
    GLM_FORCE_RADIANS
)

add_custom_command(
    TARGET main POST_BUILD

    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        $<TARGET_RUNTIME_DLLS:main>
        $<TARGET_FILE_DIR:main>
    COMMAND_EXPAND_LISTS
)