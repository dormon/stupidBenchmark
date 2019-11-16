cmake_minimum_required(VERSION 3.12.1)

project(stupidBenchmark)

SET(CMAKE_CXX_STANDARD 17)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_INCLUDE_CURRENT_DIR_IN_INTERFACE ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS 1 ) 

set(MAJOR_VERSION 1)
set(MINOR_VERSION 0)
set(REVISION_VERSION 0)

find_package(SDL2           2.0.9 CONFIG REQUIRED)
find_package(OpenCL         QUIET)
find_package(Vulkan         QUIET)

include(CMakeUtils.cmake)

createTargetForBadLibrary(OpenCL "${OpenCL_LIBRARY}" "${OpenCL_INCLUDE_DIR}")

add_subdirectory(TxtUtils)
add_subdirectory(MealyMachine)
add_subdirectory(geGL)
add_subdirectory(ArgumentViewer)

add_executable(${PROJECT_NAME} 
  src/stupidScheduler.cpp
  src/Timer.h
  )

target_include_directories(${PROJECT_NAME} PUBLIC $<INSTALL_INTERFACE:include>)
target_include_directories(${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>)
target_link_libraries(${PROJECT_NAME} PUBLIC 
  SDL2::SDL2
  SDL2::SDL2main
  geGL::geGL
  ArgumentViewer::ArgumentViewer
  OpenCL::OpenCL
  Vulkan::Vulkan
  )


