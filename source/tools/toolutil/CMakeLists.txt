add_library(
    icutu
    collationinfo.cpp
    dbgutil.cpp
    denseranges.cpp
    filestrm.c
    filetools.cpp
    flagparser.c
    package.cpp
    pkg_genc.c
    pkg_gencmn.c
    pkg_icu.cpp
    pkgitems.cpp
    ppucd.cpp
    swapimpl.cpp
    toolutil.cpp
    ucbuf.c
    ucln_tu.cpp
    ucm.c
    ucmstate.c
    udbgutil.cpp
    unewdata.c
    uoptions.c
    uparse.c
    writesrc.c
    xmlparser.cpp
)

target_compile_definitions(icutu PRIVATE U_TOOLUTIL_IMPLEMENTATION)

target_link_libraries(icutu PUBLIC icuuc icui18n)

if(U_HAVE_ELF_H)
  target_compile_definitions(icutu PUBLIC U_HAVE_ELF_H=1)
endif()

target_include_directories(
    icutu
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
)

install(
    TARGETS icutu
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

set_target_properties(icutu PROPERTIES EXPORT_NAME tu)
