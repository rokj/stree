add_executable(cmd
    cmd.cpp
    httpcredentialstext.cpp
)
set_target_properties(cmd PROPERTIES OUTPUT_NAME "${APPLICATION_EXECUTABLE}cmd")
ecm_mark_nongui_executable(cmd)

target_link_libraries(cmd csync libsync Qt::Core Qt::Network)
apply_common_target_settings(cmd)

if(APPLE)
    set_target_properties(cmd PROPERTIES RUNTIME_OUTPUT_DIRECTORY "$<TARGET_FILE_DIR:owncloud>")
else()
    install(TARGETS cmd ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})
endif()

if(UNIX AND NOT APPLE)
    configure_file(${CMAKE_SOURCE_DIR}/owncloudcmd.desktop.in ${CMAKE_CURRENT_BINARY_DIR}/${APPLICATION_EXECUTABLE}cmd.desktop)
    install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${APPLICATION_EXECUTABLE}cmd.desktop DESTINATION ${KDE_INSTALL_DATADIR}/applications)
endif()
