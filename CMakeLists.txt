cmake_minimum_required(VERSION 3.20)

project(option_operators
  VERSION 0.1.0
  LANGUAGES CXX
)

# If you want the build process to take longer, uncomment the lines below

#find_program(CLANG_TIDY_EXE NAMES clang-tidy)

#if(CLANG_TIDY_EXE)
#  set(CMAKE_CXX_CLANG_TIDY
#    ${CLANG_TIDY_EXE};
#    -quiet
#  )
#endif()

# ---------------------------------------
# Global settings
# ---------------------------------------
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# ---------------------------------------
# Library target
# ---------------------------------------
add_library(option_operators
  src/lib/dummy.cpp
)

find_program(CLANG_TIDY_EXE NAMES clang-tidy)

if(CLANG_TIDY_EXE)
  set_target_properties(option_operators PROPERTIES
    CXX_CLANG_TIDY "${CLANG_TIDY_EXE};-quiet"
  )
endif()

target_include_directories(option_operators
  PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)

target_compile_options(option_operators
  PRIVATE
    -Wall -Wextra -Wpedantic
)

# ---------------------------------------
# CLI executable
# ---------------------------------------
add_executable(oo_run
  src/cli/main.cpp
)

target_link_libraries(oo_run
  PRIVATE option_operators
)

# ---------------------------------------
# Testing
# ---------------------------------------
include(CTest)
enable_testing()

add_subdirectory(tests)
