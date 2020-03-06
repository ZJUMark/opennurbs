cmake_minimum_required(VERSION 3.9)
project(openNURBS LANGUAGES C CXX)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/modules)
include(${PROJECT_SOURCE_DIR}/cmake/Utils.cmake)
standard_config()
standard_paths(${PROJECT_SOURCE_DIR} bin lib)
set(CMAKE_CXX_STANDARD 17)

add_definitions(-DZ_PREFIX -DON_COMPILING_OPENNURBS)

set(project_link_libs)
set(project_include_dirs)

list(APPEND project_link_libs uuid)

list(APPEND project_include_dirs
	${CMAKE_SOURCE_DIR}/opennurbs/include
	${CMAKE_SOURCE_DIR}/opennurbs/zlib
)
file(GLOB project_cpp_files
	"${CMAKE_SOURCE_DIR}/opennurbs/zlib/*.c"
	"${CMAKE_SOURCE_DIR}/opennurbs/src/*.cpp"
)
set(SRC
	${HEADERS}
	${SOURCES}
	${project_cpp_files}
)

set(target_lib ${PROJECT_NAME})

add_library(${target_lib} STATIC ${SRC})

set_target_properties(${target_lib} PROPERTIES POSITION_INDEPENDENT_CODE ON)
target_include_directories(${target_lib} PUBLIC ${project_include_dirs})

target_link_libraries(${target_lib} PRIVATE ${project_link_libs})

install(TARGETS ${target_lib}
    LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib)
	
add_subdirectory(examples)