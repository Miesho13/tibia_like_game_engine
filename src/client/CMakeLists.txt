cmake_minimum_required(VERSION 3.28)

project(application_tibia)

file(GLOB app_src "${CMAKE_CURRENT_SOURCE_DIR}/*.c"
                  "${CMAKE_CURRENT_SOURCE_DIR}/../common/*.c")

add_executable(${PROJECT_NAME} ${app_src})

target_include_directories(
    ${PROJECT_NAME} PRIVATE
    ${CMAKE_BINARY_DIR}/external/raylib/raylib/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../common
)

target_link_libraries(${PROJECT_NAME} ${CMAKE_BINARY_DIR}/external/raylib/raylib/libraylib.a m)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_CURRENT_SOURCE_DIR}/resources ${CMAKE_BINARY_DIR}/src/client/resources)
