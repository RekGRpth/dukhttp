cmake_minimum_required(VERSION 3.4)
project(dukhttp LANGUAGES C)

if(CMAKE_C_COMPILER_ID MATCHES "AppleClang|Clang|GNU")
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -Os -Wall -Wextra")
  set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -flto")
endif()

add_executable(dukhttp src/main.c)

if(CMAKE_C_COMPILER_ID MATCHES "AppleClang|Clang|GNU")
  target_link_libraries(dukhttp m)
else()
  target_link_libraries(dukhttp)
endif()

target_link_libraries(dukhttp uv duktape http_parser)
target_include_directories(dukhttp PUBLIC "${PROJECT_SOURCE_DIR}/src")

if (NOT CMAKE_SKIP_INSTALL_RULES)
  install(TARGETS dukhttp
          RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR})
endif()
