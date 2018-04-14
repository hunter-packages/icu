add_executable(
    genrb
    errmsg.c
    genrb.c
    parse.cpp
    read.c
    reslist.c
    ustr.c
    rbutil.c
    wrtjava.c
    rle.c
    wrtxml.cpp
    prscmnts.cpp
)

target_link_libraries(genrb PUBLIC icutu icui18n icuuc)

install(
    TARGETS genrb
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

if(ICU_BUILD_IO)
  add_executable(derb derb.c)

  target_link_libraries(derb PUBLIC icuio icutu icui18n icuuc)

  install(
      TARGETS derb
      EXPORT "${TARGETS_EXPORT_NAME}"
      LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
      ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
      RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
      INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
  )
endif()
