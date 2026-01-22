cmake_minimum_required (VERSION 3.20 FATAL_ERROR)

project(osclib VERSION 1.2.1)

add_library(OscLib_Options INTERFACE)
target_compile_options(OscLib_Options INTERFACE -Werror -pedantic -Wno-unused-local-typedefs)

option(STAN "Build with Stan dependency")
option(USE_STAN_THREADS "Use threading with Stan?" ON)

find_package(ROOT REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(Boost REQUIRED)
find_package(GSL REQUIRED)

if(STAN)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DOSCLIB_STAN -D_REENTRANT")
  if(TBB_ONEAPI)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DTBB_INTERFACE_NEW")
  endif()
  if(USE_STAN_THREADS)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSTAN_THREADS")
  endif()
  list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
  find_package(stan_math REQUIRED)
  find_package(SUNDIALS REQUIRED)
  find_package(TBB REQUIRED)
endif()

add_subdirectory(OscLib)
