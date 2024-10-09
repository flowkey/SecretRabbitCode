cmake_minimum_required(VERSION 3.16)
set(CMAKE_Swift_MODULE_DIRECTORY ${CMAKE_BINARY_DIR}/swift)
project(SecretRabbitCode LANGUAGES Swift C)

set (LIBSAMPLERATE_DIR libsamplerate)
set(BUILD_TESTING CACHE BOOL OFF)
set(LIBSAMPLERATE_EXAMPLES OFF)
add_subdirectory (${LIBSAMPLERATE_DIR} ./libsamplerate)
include_directories(${LIBSAMPLERATE_DIR}/include)

add_library(SecretRabbitCode SHARED
    Sources/SecretRabbitCode/SecretRabbitCode.swift
)

set_target_properties(SecretRabbitCode PROPERTIES
    INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_Swift_MODULE_DIRECTORY}
    INTERFACE_INCLUDE_DIRECTORIES ./Sources/CSamplerate/
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/Sources/CSamplerate/)
add_library(CSamplerate ALIAS samplerate)

target_link_libraries(SecretRabbitCode
    PRIVATE
        CSamplerate
)

