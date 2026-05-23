cmake_minimum_required(VERSION 3.30...4.3)

project(simple_svg_ext)
include(cmake_util/dependencies.cmake)

get_filename_component(simple_svg_root_dir "${CMAKE_CURRENT_LIST_DIR}" DIRECTORY)

set(simple_svg_ext_dummy "${CMAKE_CURRENT_BINARY_DIR}/simple_svg_ext_dummy.cpp")
file(WRITE "${simple_svg_ext_dummy}" "namespace { int simple_svg_ext_dummy; }\n")

add_library(${PROJECT_NAME} STATIC
    ${simple_svg_ext_dummy}
    "${simple_svg_root_dir}/simple_svg_1.0.0.hpp"
    chart_axes.hpp
    linechart.hpp
    histchart.hpp
    simple_svg_ext.hpp
    text.hpp
)
target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_23)

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} "${simple_svg_root_dir}")
target_link_libraries(${PROJECT_NAME} PUBLIC mb::util)

file(GLOB_RECURSE ${PROJECT_NAME}_INCLUDE_FILES "*.h*")

set(${PROJECT_NAME}_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR} "${simple_svg_root_dir}"
    CACHE INTERNAL "${PROJECT_NAME}: include directories" FORCE)
