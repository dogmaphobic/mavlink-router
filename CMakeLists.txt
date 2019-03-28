cmake_minimum_required(VERSION 3.5)

project(mavlink-routerd)

execute_process(COMMAND git --git-dir ${CMAKE_CURRENT_SOURCE_DIR}/.git rev-list master --first-parent --count OUTPUT_VARIABLE BUILD_VERSION OUTPUT_STRIP_TRAILING_WHITESPACE)

add_definitions(
    -Wall
    -Wextra
    -DPACKAGE="${PROJECT_NAME}"
    -DVERSION="1.0.${BUILD_VERSION}"
)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

file(GLOB SRC_FILES src/common/*.c src/common/*.cpp src/mavlink-router/*.cpp)

add_executable(${PROJECT_NAME}
    ${SRC_FILES}
)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${CMAKE_CURRENT_SOURCE_DIR}/modules/v2/ardupilotmega
)

target_compile_options(${PROJECT_NAME} PUBLIC
    ${GST_CFLAGS}
)

