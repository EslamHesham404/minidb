cmake_minimum_required(VERSION 3.0)

project(minidb VERSION 0.1)


set(CMAKE_CXX_STANDARD 11)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set (CMAKE_VERBOSE_MAKEFILE 0) # 1 should be used for debugging
set (CMAKE_SUPPRESS_REGENERATION TRUE) # Suppresses ZERO_CHECK

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -lpthread -W")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -Wall")

if(MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -W4")
  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -Wall")
endif()


message("Generated with config types: ${CMAKE_CONFIGURATION_TYPES}")

include_directories (src/
                     include/
                    # Add More Direct. Here if needed.
                    )

# Add Files
file (GLOB_RECURSE PROJECT_HEADERS src/*.hpp
                    src/*.h)
file (GLOB_RECURSE PROJECT_SOURCES src/*.cpp
                    src/*.cxx
                    src/*.cc
                    src/*.c)
file (GLOB         PROJECT_CONFIGS CMakeLists.txt)

#
# Organizing files
#
source_group ("headers" FILES ${PROJECT_HEADERS})
source_group ("sources" FILES ${PROJECT_SOURCES})
source_group ("vendors" FILES ${VENDORS_SOURCES})

add_executable (${PROJECT_NAME} ${PROJECT_SOURCES} ${PROJECT_HEADERS}
                                ${COMMON_SOURCES} ${COMMON_HEADERS}
                                ${PROJECT_CONFIGS} ${VENDORS_SOURCES})
set_target_properties (${PROJECT_NAME} PROPERTIES
                                RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${PROJECT_NAME})
