set(sources)
if(NOT ICU_WINDOWS_STORE)
  list(APPEND sources icuplug.cpp wintz.cpp)
endif()

add_library(
    icuuc
    ${sources}
    appendable.cpp
    bmpset.cpp
    bmpset.h
    brkeng.cpp
    brkeng.h
    brkiter.cpp
    bytesinkutil.cpp
    bytestream.cpp
    bytestrie.cpp
    bytestriebuilder.cpp
    bytestrieiterator.cpp
    caniter.cpp
    characterproperties.cpp
    chariter.cpp
    charstr.cpp
    charstr.h
    cmemory.cpp
    cmemory.h
    cpputils.h
    cstr.cpp
    cstring.cpp
    cstring.h
    cwchar.cpp
    cwchar.h
    dictbe.cpp
    dictbe.h
    dictionarydata.cpp
    dtintrv.cpp
    edits.cpp
    errorcode.cpp
    filteredbrk.cpp
    filterednormalizer2.cpp
    hash.h
    icudataver.cpp
    icuplugimp.h
    loadednormalizer2impl.cpp
    localsvc.h
    locavailable.cpp
    locbased.cpp
    locbased.h
    locdispnames.cpp
    locdspnm.cpp
    locid.cpp
    loclikely.cpp
    locmap.cpp
    locmap.h
    locresdata.cpp
    locutil.cpp
    locutil.h
    messagepattern.cpp
    msvcres.h
    mutex.h
    normalizer2.cpp
    normalizer2impl.cpp
    normalizer2impl.h
    normlzr.cpp
    parsepos.cpp
    patternprops.cpp
    pluralmap.cpp
    propname.cpp
    propname.h
    propsvec.cpp
    propsvec.h
    punycode.cpp
    punycode.h
    putil.cpp
    putilimp.h
    rbbi.cpp
    rbbi_cache.cpp
    rbbidata.cpp
    rbbidata.h
    rbbinode.cpp
    rbbinode.h
    rbbirb.cpp
    rbbirb.h
    rbbirpt.h
    rbbiscan.cpp
    rbbiscan.h
    rbbisetb.cpp
    rbbisetb.h
    rbbistbl.cpp
    rbbitblb.cpp
    rbbitblb.h
    resbund.cpp
    resbund_cnv.cpp
    resource.cpp
    ruleiter.cpp
    ruleiter.h
    schriter.cpp
    serv.cpp
    serv.h
    servlk.cpp
    servlkf.cpp
    servloc.h
    servls.cpp
    servnotf.cpp
    servnotf.h
    servrbf.cpp
    servslkf.cpp
    sharedobject.cpp
    simpleformatter.cpp
    sprpimpl.h
    static_unicode_sets.cpp
    stringpiece.cpp
    stringtriebuilder.cpp
    uarrsort.cpp
    uarrsort.h
    uassert.h
    ubidi.cpp
    ubidi_props.cpp
    ubidi_props.h
    ubidiimp.h
    ubidiln.cpp
    ubiditransform.cpp
    ubidiwrt.cpp
    ubrk.cpp
    ubrkimpl.h
    ucase.cpp
    ucase.h
    ucasemap.cpp
    ucasemap_titlecase_brkiter.cpp
    ucat.cpp
    uchar.cpp
    ucharstrie.cpp
    ucharstriebuilder.cpp
    ucharstrieiterator.cpp
    uchriter.cpp
    ucln.h
    ucln_cmn.cpp
    ucln_cmn.h
    ucln_imp.h
    ucmndata.cpp
    ucmndata.h
    ucnv.cpp
    ucnv2022.cpp
    ucnv_bld.cpp
    ucnv_bld.h
    ucnv_cb.cpp
    ucnv_cnv.cpp
    ucnv_cnv.h
    ucnv_ct.cpp
    ucnv_err.cpp
    ucnv_ext.cpp
    ucnv_ext.h
    ucnv_imp.h
    ucnv_io.cpp
    ucnv_io.h
    ucnv_lmb.cpp
    ucnv_set.cpp
    ucnv_u16.cpp
    ucnv_u32.cpp
    ucnv_u7.cpp
    ucnv_u8.cpp
    ucnvbocu.cpp
    ucnvdisp.cpp
    ucnvhz.cpp
    ucnvisci.cpp
    ucnvlat1.cpp
    ucnvmbcs.cpp
    ucnvmbcs.h
    ucnvscsu.cpp
    ucnvsel.cpp
    ucol_swp.cpp
    ucol_swp.h
    ucptrie.cpp
    ucurr.cpp
    udata.cpp
    udatamem.cpp
    udatamem.h
    udataswp.cpp
    udataswp.h
    uenum.cpp
    uenumimp.h
    uhash.cpp
    uhash.h
    uhash_us.cpp
    uidna.cpp
    uinit.cpp
    uinvchar.cpp
    uinvchar.h
    uiter.cpp
    ulist.cpp
    ulist.h
    uloc.cpp
    uloc_keytype.cpp
    uloc_tag.cpp
    ulocimp.h
    umapfile.cpp
    umapfile.h
    umath.cpp
    umutablecptrie.cpp
    umutex.cpp
    umutex.h
    unames.cpp
    unifiedcache.cpp
    unifilt.cpp
    unifunct.cpp
    uniset.cpp
    uniset_closure.cpp
    uniset_props.cpp
    unisetspan.cpp
    unisetspan.h
    unistr.cpp
    unistr_case.cpp
    unistr_case_locale.cpp
    unistr_cnv.cpp
    unistr_props.cpp
    unistr_titlecase_brkiter.cpp
    unorm.cpp
    unormcmp.cpp
    unormimp.h
    uobject.cpp
    uprops.cpp
    uprops.h
    ures_cnv.cpp
    uresbund.cpp
    uresdata.cpp
    uresdata.h
    uresimp.h
    ureslocs.h
    usc_impl.cpp
    usc_impl.h
    uscript.cpp
    uscript_props.cpp
    uset.cpp
    uset_imp.h
    uset_props.cpp
    usetiter.cpp
    ushape.cpp
    usprep.cpp
    ustack.cpp
    ustr_cnv.cpp
    ustr_cnv.h
    ustr_imp.h
    ustr_titlecase_brkiter.cpp
    ustr_wcs.cpp
    ustrcase.cpp
    ustrcase_locale.cpp
    ustrenum.cpp
    ustrenum.h
    ustrfmt.cpp
    ustrfmt.h
    ustring.cpp
    ustrtrns.cpp
    utext.cpp
    utf_impl.cpp
    util.cpp
    util.h
    util_props.cpp
    utrace.cpp
    utracimp.h
    utrie.cpp
    utrie.h
    utrie2.cpp
    utrie2.h
    utrie2_builder.cpp
    utrie2_impl.h
    utrie_swap.cpp
    uts46.cpp
    utypes.cpp
    uvector.cpp
    uvector.h
    uvectr32.cpp
    uvectr32.h
    uvectr64.cpp
    uvectr64.h
    wintz.h
)

target_compile_definitions(icuuc PRIVATE U_COMMON_IMPLEMENTATION)

target_compile_definitions(
    icuuc
    PUBLIC
    UNISTR_FROM_CHAR_EXPLICIT=explicit
    UNISTR_FROM_STRING_EXPLICIT=explicit
    U_HAVE_ATOMIC=1
)

if(U_NO_DEFAULT_INCLUDE_UTF_HEADERS)
  target_compile_definitions(
      icuuc
      PUBLIC
      U_NO_DEFAULT_INCLUDE_UTF_HEADERS=1
  )
endif()

target_link_libraries(icuuc PUBLIC ${CMAKE_DL_LIBS})

if(ICU_DATA_ARCHIVE_MODE)
  target_link_libraries(icuuc PUBLIC icustubdata)
else()
  # INSTALL_INTERFACE introduced to avoid cyclic dependency:
  # * icupkg -> icuuc -> icudata -> icupkg (generated by)
  # Build:
  # * icudata -> icupkg -> icuuc -> icustubdata
  # Usage:
  # * icuuc -> icudata
  target_link_libraries(icuuc PUBLIC $<BUILD_INTERFACE:icustubdata>)
  target_link_libraries(icuuc PUBLIC $<INSTALL_INTERFACE:icudata>)
endif()

if(U_USING_ICU_NAMESPACE)
  target_compile_definitions(icuuc PUBLIC U_USING_ICU_NAMESPACE=1)
else()
  target_compile_definitions(icuuc PUBLIC U_USING_ICU_NAMESPACE=0)
endif()

if(NOT BUILD_SHARED_LIBS)
  if(MSVC)
    target_compile_definitions(icuuc PUBLIC U_STATIC_IMPLEMENTATION)
  else()
    target_compile_definitions(icuuc PUBLIC $<BUILD_INTERFACE:U_STATIC_IMPLEMENTATION>)
  endif()
endif()

if(MSVC)
  target_compile_definitions(icuuc PUBLIC U_PLATFORM_USES_ONLY_WIN32_API=1)
  if(ICU_WINDOWS_STORE)
    target_compile_definitions(icuuc PUBLIC U_PLATFORM_HAS_WINUWP_API=1)
  else()
    target_compile_definitions(icuuc PUBLIC U_PLATFORM_HAS_WINUWP_API=0)
  endif()
endif()

target_include_directories(
    icuuc
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
)

install(
    DIRECTORY unicode
    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
    FILES_MATCHING
    PATTERN "*.h"
)

install(
    TARGETS icuuc
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

set_target_properties(icuuc PROPERTIES EXPORT_NAME uc)
