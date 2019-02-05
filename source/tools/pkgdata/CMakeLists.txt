add_executable(pkgdata pkgdata.cpp pkgtypes.c)

target_link_libraries(pkgdata PUBLIC icutu icui18n icuuc)

install(
    TARGETS pkgdata
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)
