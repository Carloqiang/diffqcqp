cmake_minimum_required(VERSION 3.0.0)
project(diffsolvers VERSION 0.1.0)

include(CTest)
enable_testing()

find_package(pybind11 REQUIRED)
find_package(Eigen3 3.3 REQUIRED)
find_package(Python3 3.7.6 REQUIRED)

add_subdirectory(qcqplib)

add_executable(diffsolver main.cpp)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

target_link_libraries(diffsolver qcqplib)

pybind11_add_module(pybindings pybindings.cpp)
target_link_libraries(pybindings PRIVATE Eigen3::Eigen)
target_link_libraries(pybindings PRIVATE qcqplib)
target_compile_options(pybindings PRIVATE -fPIC)
