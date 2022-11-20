cmake_minimum_required(VERSION 3.14)

# set(CMAKE_CXX_STANDARD 17)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_STATIC_RUNTIME ON)
set(Boost_NO_SYSTEM_PATHS TRUE)
set(Boost_USE_STATIC_LIBS TRUE)

include(cpk-cmake/cpk.cmake)

project(boost-dll-playground)

SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static")

add_executable(${PROJECT_NAME}
    "src/main.cpp"
    "src/plugin.hpp"
)

add_library("${PROJECT_NAME}_plugin" SHARED
    "src/plugin.cpp"
    "src/plugin.hpp"
)

cpk_add(${PROJECT_NAME} Boost 1.80.0 a Boost::boost)

target_link_libraries(${PROJECT_NAME} ws2_32)


cpk_add("${PROJECT_NAME}_plugin" Boost 1.80.0 a Boost::boost)

target_link_libraries("${PROJECT_NAME}_plugin" ws2_32)