cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

project(imgui VERSION 1.53 LANGUAGES CXX)
option (BUILD_SHARED_LIBS "Build shared (dynamic) libraries." ON)

set(PROJECT_SOURCES
  imconfig.h
  imgui.h
  imgui_internal.h
  stb_rect_pack.h
  stb_textedit.h
  stb_truetype.h

  imgui.cpp
  imgui_demo.cpp
  imgui_draw.cpp
)

add_library(${PROJECT_NAME} ${PROJECT_SOURCES})
target_include_directories(${PROJECT_NAME} PUBLIC 
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>
  $<INSTALL_INTERFACE:include> PRIVATE source)

install(TARGETS ${PROJECT_NAME} EXPORT "${PROJECT_NAME}-config"
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin)
install(DIRECTORY "include/"               DESTINATION "include")
install(EXPORT    "${PROJECT_NAME}-config" DESTINATION "cmake"  )
export (TARGETS   "${PROJECT_NAME}"        FILE        "${PROJECT_NAME}-config.cmake")
