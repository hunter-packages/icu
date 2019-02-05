# See Makefile.in
install(
    DIRECTORY layout
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
    FILES_MATCHING
    PATTERN "*.h"
)

add_library(
    iculx
    ParagraphLayout.cpp
    RunArrays.cpp
    LXUtilities.cpp
    playout.cpp
    plruns.cpp
)

target_compile_definitions(iculx PRIVATE U_LAYOUTEX_IMPLEMENTATION)

target_link_libraries(iculx PUBLIC icule)

target_include_directories(
    iculx
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
)

install(
    TARGETS iculx
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

set_target_properties(iculx PROPERTIES EXPORT_NAME lx)
