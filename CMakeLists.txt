cmake_minimum_required(VERSION 3.15)
set(PROJECT_NAME Verlet)
project(${PROJECT_NAME} VERSION 2.0.0 LANGUAGES CXX)

set(SOURCES main.cpp)

# Detect and add SFML 
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake_modules" ${CMAKE_MODULE_PATH})
find_package(SFML 2.5 REQUIRED COMPONENTS network audio graphics window system)

add_executable(${PROJECT_NAME} ${SOURCES})
target_link_libraries(${PROJECT_NAME} sfml-system sfml-window sfml-graphics)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 17)

if (UNIX)
    target_link_libraries(${PROJECT_NAME} pthread)
endif (UNIX)

if(NOT SFML_FOUND)
    message(FATAL_ERROR "SFML not found. Please make sure SFML is installed and set CMAKE_PREFIX_PATH to SFML's installation path.")
endif()
