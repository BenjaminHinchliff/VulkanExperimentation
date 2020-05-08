# CMakeList.txt : CMake project for Vulkan, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project ("Vulkan")

# copy files
configure_file("shaders/shader.vert.spv" "shaders/shader.vert.spv" COPYONLY)
configure_file("shaders/shader.frag.spv" "shaders/shader.frag.spv" COPYONLY)
configure_file("textures/texture.jpg" "textures/texture.jpg" COPYONLY)
configure_file("textures/viking_room.png" "textures/viking_room.png" COPYONLY)
configure_file("models/viking_room.wobj" "models/viking_room.wobj" COPYONLY)

add_executable (main "Vulkan.cpp")

# find and link vulkan
find_package(Vulkan REQUIRED)
target_link_libraries(main PRIVATE Vulkan::Vulkan)

# add glfw
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
add_subdirectory("deps/glfw-3.3.2")
target_link_libraries(main PRIVATE glfw)

# add glm
add_subdirectory("deps/glm-0.9.9.8")
target_link_libraries(main PRIVATE glm)

# include stb
target_include_directories(main PRIVATE "deps/stb")

# include tiny_obj_loader
target_include_directories(main PRIVATE "deps/tiny_obj_loader")