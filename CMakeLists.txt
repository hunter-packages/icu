# Copyright (c) 2014, 2018-2019, Ruslan Baratov
# All rights reserved.

cmake_minimum_required(VERSION 3.2)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.23.97.tar.gz"
    SHA1 "91125b6ac0df9be4c2b7a5695e58d94a0e8a74e3"
)

project(ICU VERSION 63.1 LANGUAGES C CXX ASM)

set(CMAKE_CXX_STANDARD 11 CACHE STRING "Default C++ standard")

string(COMPARE EQUAL "${CMAKE_SYSTEM_NAME}" "WindowsStore" ICU_WINDOWS_STORE)

if(IOS OR ANDROID OR ICU_WINDOWS_STORE)
  set(default OFF)
else()
  set(default ON)
endif()

if(MSVC)
  add_definitions(-D_CRT_SECURE_NO_WARNINGS)
  add_definitions(-D_CRT_SECURE_NO_DEPRECATE)
  add_definitions(-DU_ATTRIBUTE_DEPRECATED=)
  add_definitions(/utf-8)
endif()

option(ICU_BUILD_TOOLS "Build ICU tools" ${default})

option(ICU_BUILD_IO "Build IO library" OFF)

option(ICU_DATA_ARCHIVE_MODE "Output a single icudt*.dat file" OFF)

option(U_NO_DEFAULT_INCLUDE_UTF_HEADERS "..." OFF)

option(U_USING_ICU_NAMESPACE "..." OFF)

include(CheckIncludeFile)
check_include_file(elf.h U_HAVE_ELF_H)

set(ICU_DATA_FILE_NAME icudt${PROJECT_VERSION_MAJOR}l.dat)

set(icu_data_local_dir ${CMAKE_CURRENT_LIST_DIR}/source/data/in)
set(ICU_DATA_LOCAL_FILE ${icu_data_local_dir}/${ICU_DATA_FILE_NAME})
if(NOT EXISTS ${ICU_DATA_LOCAL_FILE})
  message(FATAL_ERROR "File not found: ${ICU_DATA_LOCAL_FILE}")
endif()

set(ICU_DATA_INSTALL_DIR share/icu/${PROJECT_VERSION})

### Installation (https://github.com/forexample/package-example) {

# Introduce variables:
# * CMAKE_INSTALL_LIBDIR
# * CMAKE_INSTALL_BINDIR
# * CMAKE_INSTALL_INCLUDEDIR
include(GNUInstallDirs)

set(config_install_dir "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}")
set(generated_dir "${CMAKE_CURRENT_BINARY_DIR}/generated")
set(version_config "${generated_dir}/${PROJECT_NAME}ConfigVersion.cmake")
set(project_config "${generated_dir}/${PROJECT_NAME}Config.cmake")
set(TARGETS_EXPORT_NAME "${PROJECT_NAME}Targets")
set(namespace "${PROJECT_NAME}::")

include(CMakePackageConfigHelpers)

# Use:
# * PROJECT_VERSION
write_basic_package_version_file(
    "${version_config}" COMPATIBILITY SameMajorVersion
)

# Use:
# * TARGETS_EXPORT_NAME
# * PROJECT_NAME
configure_package_config_file(
    "cmake/template/Config.cmake.in"
    "${project_config}"
    INSTALL_DESTINATION "${config_install_dir}"
)

install(
    FILES "${project_config}" "${version_config}"
    DESTINATION "${config_install_dir}"
)

install(
    EXPORT "${TARGETS_EXPORT_NAME}"
    NAMESPACE "${namespace}"
    DESTINATION "${config_install_dir}"
)

### }

### RPATH settings {

# https://cmake.org/Wiki/CMake_RPATH_handling
if(IOS)
  # TODO: iOS dynamic framework
elseif(ANDROID)
  # *.so libraries loaded by Java code, RPATH will not be used
elseif(UNIX)
  if(APPLE)
    # https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/dyld.1.html
    set(CMAKE_INSTALL_RPATH "@executable_path/../${CMAKE_INSTALL_LIBDIR}")
  else()
    # https://linux.die.net/man/8/ld-linux
    set(CMAKE_INSTALL_RPATH "\$ORIGIN/../${CMAKE_INSTALL_LIBDIR}")
  endif()
endif()

### }

add_subdirectory(source/common) # icuuc

# Not used, see:
# - https://docs.hunter.sh/en/latest/packages/pkg/icu-lx.html
# add_subdirectory(source/layoutex) # iculx

add_subdirectory(source/i18n) # icui18n

if(ICU_BUILD_IO)
  add_subdirectory(source/io) # icuio
endif()

if(ICU_BUILD_TOOLS)
  add_subdirectory(source/tools)
endif()

add_subdirectory(source/stubdata)

if(ICU_DATA_ARCHIVE_MODE)
  install(FILES ${ICU_DATA_LOCAL_FILE} DESTINATION ${ICU_DATA_INSTALL_DIR})
else()
  add_subdirectory(source/data) # after 'tools'
endif()
