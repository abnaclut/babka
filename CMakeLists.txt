cmake_minimum_required(VERSION 3.13 FATAL_ERROR)

set(PROJECT_NAME openTemplate)
project(${PROJECT_NAME})

add_executable(${PROJECT_NAME}
        src/main.cpp
        src/Renderer/ShaderProgram.cpp
        src/Renderer/ShaderProgram.h
        src/Resources/ResourceManager.cpp
        src/Resources/ResourceManager.h
        src/Resources/stb_image.h
        src/Renderer/Texture2D.cpp
        src/Renderer/Texture2D.h
)

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)

add_subdirectory(external/glfw)
add_subdirectory(external/glad)
add_subdirectory(external/glm)

target_link_libraries(${PROJECT_NAME} glfw)
target_link_libraries(${PROJECT_NAME} glad)
target_link_libraries(${PROJECT_NAME} glm)

include_directories(external/glm/glm)

set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/res $<TARGET_FILE_DIR:${PROJECT_NAME}>/res)