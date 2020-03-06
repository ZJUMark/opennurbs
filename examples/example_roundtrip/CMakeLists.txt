set(executor_name example_roundtrip)

remove_definitions(-DON_COMPILING_OPENNURBS)

file(GLOB CPPFILES
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/../example_userdata/example_ud.cpp"
)

include_directories(
    "${CMAKE_SOURCE_DIR}/opennurbs/include"
    "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_executable(${executor_name} ${CPPFILES})
target_link_libraries(${executor_name} PRIVATE ${PROJECT_NAME})