# CMakeList.txt : CMake project for Vulkan, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project ("Vulkan")

# copy shaders using configure file
configure_file("shaders/vert.spv" "shaders/vert.spv" COPYONLY)
configure_file("shaders/frag.spv" "shaders/frag.spv" COPYONLY)

add_executable (main "Vulkan.cpp")

find_package(Vulkan REQUIRED)
target_link_libraries(main PRIVATE Vulkan::Vulkan)

find_package(glfw3 CONFIG REQUIRED)
target_link_libraries(main PRIVATE glfw)

find_package(glm CONFIG REQUIRED)
target_link_libraries(main PRIVATE glm)