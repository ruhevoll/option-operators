include(FetchContent)

FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG v3.5.2
)

FetchContent_MakeAvailable(Catch2)

add_executable(test_basic
  test_basic.cpp
)

target_link_libraries(test_basic
  PRIVATE
    option_operators
    Catch2::Catch2WithMain
)

add_test(NAME test_basic COMMAND test_basic)
