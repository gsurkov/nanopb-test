cmake_minimum_required(VERSION 3.16)
project("nanopb_test" C CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/nanopb/extra")

find_package(Nanopb REQUIRED)

add_library(protobuf STATIC)

file(GLOB PROTO_FILES
    "proto/*.proto"
)

nanopb_generate_cpp(
    PROTO_SOURCES
    PROTO_HEADERS
    ${PROTO_FILES}
)

target_include_directories(protobuf
    PUBLIC
        ${NANOPB_INCLUDE_DIRS}
        ${CMAKE_CURRENT_BINARY_DIR}
)

target_compile_definitions(protobuf
    PUBLIC
        "-DPB_ENABLE_MALLOC"
)

target_sources(protobuf
    PRIVATE
        ${PROTO_SOURCES}
)
