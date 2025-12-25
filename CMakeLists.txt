cmake_minimum_required(VERSION 3.10)

project(option-operators)

add_executable(option-operators main.cpp)

install(TARGETS option-operators RUNTIME DESTINATION bin)
