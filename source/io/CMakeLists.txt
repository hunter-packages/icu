add_library(
    icuio
    locbund.cpp
    sprintf.cpp
    sscanf.cpp
    ucln_io.cpp
    ufile.cpp
    ufmt_cmn.cpp
    uprintf.cpp
    uprntf_p.cpp
    uscanf.cpp
    uscanf_p.cpp
    ustdio.cpp
    ustream.cpp
)

target_compile_definitions(icuio PRIVATE U_IO_IMPLEMENTATION)

target_link_libraries(icuio PUBLIC icuuc icui18n)

target_include_directories(
    icuio
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
)

install(
    DIRECTORY "unicode"
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
    FILES_MATCHING
    PATTERN "*.h"
)

install(
    TARGETS icuio
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

set_target_properties(icuio PROPERTIES EXPORT_NAME io)
