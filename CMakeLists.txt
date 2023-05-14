# Undo Library
# Copyright (C) 2015-2022 David Capello

cmake_minimum_required(VERSION 3.2)

project(undo CXX)
option(UNDO_TESTS "Compile undo tests" on)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(
    GLOB_RECURSE sources
    LIST_DIRECTORIES false
    RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
    undo_history.cpp
)

file(
    GLOB_RECURSE public_headers
    LIST_DIRECTORIES false
    RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
    undo_command.h undo_history.h undo_state.h
)

add_library(undo STATIC ${sources} ${public_headers})

target_include_directories(undo PUBLIC ${public_headers})

set_target_properties(undo PROPERTIES 
    PUBLIC_HEADER "${public_headers}"
)

if(UNDO_TESTS)
  enable_testing()
  add_subdirectory(tests)
endif()
