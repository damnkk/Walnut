
file(GLOB_RECURSE WALNUT_SOURCES Walnut/src/*.cpp)
file(GLOB_RECURSE WALNUT_HEADERS Walnut/src/*.h)

file(GLOB IMGUI_SOURCE ${CMAKE_CURRENT_LIST_DIR}/vendor/imgui/*.cpp)
file(GLOB_RECURSE IMGUI_Header ${CMAKE_CURRENT_LIST_DIR}/vendor/*.h)
message("${IMGUI_SOURCE}")

list(APPEND WALNUT_SOURCES ${IMGUI_SOURCE})
message("${WALNUT_SOURCES}")
message("${WALNUT_HEADERS}")
add_library(Walnut STATIC ${WALNUT_SOURCES} ${WALNUT_HEADERS})
target_compile_definitions(Walnut PUBLIC WL_PLATFORM_WINDOWS)

add_subdirectory("${CMAKE_CURRENT_LIST_DIR}/vendor/GLFW")
add_subdirectory("${CMAKE_CURRENT_LIST_DIR}/vendor/glm")

target_link_libraries(Walnut PUBLIC 
    Vulkan::Vulkan
    glfw
    glm
)
message("${CMAKE_CURRENT_LIST_DIR}/src")
target_include_directories(Walnut PUBLIC 
    "${CMAKE_CURRENT_LIST_DIR}/Walnut/src"
    "${CMAKE_CURRENT_LIST_DIR}/vendor/GLFW/include"
    "${CMAKE_CURRENT_LIST_DIR}/vendor/glm"
    "${CMAKE_CURRENT_LIST_DIR}/vendor/stb_image"
    "${CMAKE_CURRENT_LIST_DIR}/vendor/imgui"
)
