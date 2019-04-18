set(submodule_name testProgs)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/../groupsock/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../liveMedia/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../UsageEnvironment/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../BasicUsageEnvironment/include)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} ${submodule_name}_src)

foreach (item ${${submodule_name}_src})
    get_filename_component(exe_name ${item} NAME_WE ".cpp")
    add_executable(${exe_name} ${item})
    target_link_libraries(${exe_name} liveMedia groupsock BasicUsageEnvironment UsageEnvironment)
    install(TARGETS ${exe_name}
            RUNTIME DESTINATION ${CMAKE_PREFIX_PATH}/bin
            PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ GROUP_EXECUTE GROUP_READ)
endforeach ()