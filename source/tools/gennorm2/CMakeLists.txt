add_executable(gennorm2 gennorm2.cpp n2builder.cpp extradata.cpp norms.cpp)

target_link_libraries(gennorm2 icutu icui18n icuuc)

install(
    TARGETS gennorm2
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)
