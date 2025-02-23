cmake_minimum_required (VERSION 3.5)

project (process_utils)

add_library (${PROJECT_NAME} STATIC src/process_utils.cpp)
add_library (aduc::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

#
# Turn -fPIC on, in order to use this library in another shared library.
#
set_property (TARGET ${PROJECT_NAME} PROPERTY POSITION_INDEPENDENT_CODE ON)

target_include_directories (${PROJECT_NAME} PUBLIC inc)

find_package (azure_c_shared_utility REQUIRED)

target_link_libraries (${PROJECT_NAME} PUBLIC aziotsharedutil PRIVATE aduc::logging aduc::c_utils aduc::config_utils aduc::string_utils)

if (ADUC_BUILD_UNIT_TESTS)
    add_subdirectory (tests)
    add_subdirectory (test_helper)
endif ()
