include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../groupsock/include)

set(submodule_name UsageEnvironment)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} ${submodule_name}_src)

add_library(${submodule_name} ${lib_style} ${${submodule_name}_src})

install(TARGETS ${submodule_name}
        ARCHIVE DESTINATION ${CMAKE_PREFIX_PATH}/lib)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
        DESTINATION ${CMAKE_PREFIX_PATH}/include/${submodule_name}
        FILES_MATCHING PATTERN "*.h*")