set(temp_dir ${CMAKE_CURRENT_BINARY_DIR}/generated)

set(data_list ${temp_dir}/icudata.lst)
set(input_dat ${ICU_DATA_LOCAL_FILE})
set(extracted_data_dir ${temp_dir}/extracted)
set(icupkg_in ${temp_dir}/icupkg.in)

if(NOT EXISTS ${input_dat})
  message(FATAL_ERROR "File doesn't exist: ${input_dat}")
endif()

set(assembler_dir ${temp_dir}/assembler) # unused
set(assembler_temp_dir ${temp_dir}/assembler_temp_dir)

set(asm_name "icudt${PROJECT_VERSION_MAJOR}l")
if(WIN32)
  set(asm_file ${assembler_temp_dir}/${asm_name}_dat.obj)
else()
  set(asm_file ${assembler_temp_dir}/${asm_name}_dat.S)
endif()

file(MAKE_DIRECTORY ${extracted_data_dir})
file(MAKE_DIRECTORY ${assembler_temp_dir})
file(MAKE_DIRECTORY ${assembler_dir})

if(CMAKE_HOST_WIN32)
  # protection not needed
  set(extract_pattern *)
else()
  set(extract_pattern \\*)
endif()

if(CMAKE_CROSSCOMPILING)
  if(ICU_WINDOWS_STORE)
    # Use same 32/64 bit Visual Studio generator
    set(HUNTER_EXPERIMENTAL_HOST_GENERATOR "${CMAKE_GENERATOR}")
  endif()

  # When cross-compiling pkgdata/icupkg tools build with host toolchain
  include(hunter_experimental_add_host_project)
  hunter_experimental_add_host_project(cmake/host)

  set(ICU_PKGDATA_EXECUTABLE "${HUNTER_HOST_ROOT}/bin/pkgdata")
  set(ICU_ICUPKG_EXECUTABLE "${HUNTER_HOST_ROOT}/bin/icupkg")
else()
  set(ICU_PKGDATA_EXECUTABLE pkgdata)
  set(ICU_ICUPKG_EXECUTABLE icupkg)
endif()

set(copy_dependent_libraries "")

if(WIN32 AND NOT CMAKE_CROSSCOMPILING)
  # FIXME: How to set PATH environment variable in custom command?
  foreach(executable icupkg pkgdata)
    foreach(dependency icutu icui18n icuuc icustubdata)
      list(
          APPEND
          copy_dependent_libraries
          COMMAND
          ${CMAKE_COMMAND}
          -E
          copy
          $<TARGET_FILE:${dependency}>
          $<TARGET_FILE_DIR:${executable}>
      )
    endforeach()
  endforeach()
endif()

add_custom_command(
    OUTPUT ${data_list}
    ${copy_dependent_libraries}
    COMMAND
        ${ICU_ICUPKG_EXECUTABLE}
        --destdir ${extracted_data_dir}
        --list
        --extract ${extract_pattern}
        ${input_dat}
        --outlist ${data_list}
    DEPENDS ${input_dat} ${ICU_ICUPKG_EXECUTABLE}
    COMMENT "Generating ${data_list} file from ${input_dat}"
)

if(APPLE)
  set(GENCCODE_ASSEMBLY_TYPE -a gcc-darwin)
elseif(UNIX)
  set(GENCCODE_ASSEMBLY_TYPE -a gcc)
else()
  set(GENCCODE_ASSEMBLY_TYPE "")
endif()

# See source/data/pkgdataMakefile.in
# Use variables:
# * GENCCODE_ASSEMBLY_TYPE
configure_file(icupkg.cmake.in ${icupkg_in} @ONLY)

if(ICU_DATA_ARCHIVE_MODE)
  set(library_type archive)
else()
  if(BUILD_SHARED_LIBS)
    set(library_type library)
  else()
    set(library_type static)
  endif()
endif()

# We only interested in generated assembler file.
# Variables like compiler/ranlib/linker/... set to dummy echo commands
add_custom_command(
    OUTPUT ${asm_file}
    COMMAND
        ${ICU_PKGDATA_EXECUTABLE}
        --bldopt ${icupkg_in}
        --copyright
        --sourcedir ${extracted_data_dir}
        --destdir ${assembler_dir}
        --entrypoint icudt${PROJECT_VERSION_MAJOR}
        --tempdir ${assembler_temp_dir}
        --name ${asm_name}
        -m ${library_type}
        --revision ${PROJECT_VERSION}
        --libname icudata
        ${data_list}
    DEPENDS ${data_list} ${ICU_PKGDATA_EXECUTABLE} ${icupkg_in}
    COMMENT "Generating ${asm_file} assembler file"
)

add_library(icudata ${asm_file})

# Name expected by Boost
if(MSVC)
  set(output_name icudt)
else()
  set(output_name icudata)
endif()

set_target_properties(
    icudata
    PROPERTIES
    LINKER_LANGUAGE C
    EXPORT_NAME data
    OUTPUT_NAME ${output_name}
)

if(MSVC AND BUILD_SHARED_LIBS)
  set_property(TARGET icudata APPEND PROPERTY LINK_FLAGS /NOENTRY)
endif()

if(NOT BUILD_SHARED_LIBS)
  target_compile_definitions(icudata PUBLIC $<BUILD_INTERFACE:U_STATIC_IMPLEMENTATION>)
endif()

install(
    TARGETS icudata
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)
