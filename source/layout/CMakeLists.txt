# See Makefile.in
install(
    FILES
    LEFontInstance.h
    LEGlyphFilter.h
    LEGlyphStorage.h
    LEInsertionList.h
    LELanguages.h
    LEScripts.h
    LESwaps.h
    LETableReference.h
    LETypes.h
    LayoutEngine.h
    loengine.h
    DESTINATION
    ${CMAKE_INSTALL_INCLUDEDIR}/layout
)

add_library(
    icule
    AlternateSubstSubtables.cpp
    AnchorTables.cpp
    ArabicLayoutEngine.cpp
    ArabicShaping.cpp
    CanonData.cpp
    CanonShaping.cpp
    ClassDefinitionTables.cpp
    ContextualGlyphInsertionProc2.cpp
    ContextualGlyphSubstProc.cpp
    ContextualGlyphSubstProc2.cpp
    ContextualSubstSubtables.cpp
    CoverageTables.cpp
    CursiveAttachmentSubtables.cpp
    DeviceTables.cpp
    ExtensionSubtables.cpp
    Features.cpp
    GDEFMarkFilter.cpp
    GXLayoutEngine.cpp
    GXLayoutEngine2.cpp
    GlyphDefinitionTables.cpp
    GlyphIterator.cpp
    GlyphLookupTables.cpp
    GlyphPositionAdjustments.cpp
    GlyphPositioningTables.cpp
    GlyphPosnLookupProc.cpp
    GlyphSubstLookupProc.cpp
    GlyphSubstitutionTables.cpp
    HanLayoutEngine.cpp
    HangulLayoutEngine.cpp
    IndicClassTables.cpp
    IndicLayoutEngine.cpp
    IndicRearrangementProcessor.cpp
    IndicRearrangementProcessor2.cpp
    IndicReordering.cpp
    KernTable.cpp
    KhmerLayoutEngine.cpp
    KhmerReordering.cpp
    LEFontInstance.cpp
    LEGlyphStorage.cpp
    LEInsertionList.cpp
    LayoutEngine.cpp
    LigatureSubstProc.cpp
    LigatureSubstProc2.cpp
    LigatureSubstSubtables.cpp
    LookupProcessor.cpp
    LookupTables.cpp
    Lookups.cpp
    MPreFixups.cpp
    MarkArrays.cpp
    MarkToBasePosnSubtables.cpp
    MarkToLigaturePosnSubtables.cpp
    MarkToMarkPosnSubtables.cpp
    MirroredCharData.cpp
    MorphTables.cpp
    MorphTables2.cpp
    MultipleSubstSubtables.cpp
    NonContextualGlyphSubstProc.cpp
    NonContextualGlyphSubstProc2.cpp
    OpenTypeLayoutEngine.cpp
    OpenTypeUtilities.cpp
    PairPositioningSubtables.cpp
    ScriptAndLanguage.cpp
    ScriptAndLanguageTags.cpp
    SegmentArrayProcessor.cpp
    SegmentArrayProcessor2.cpp
    SegmentSingleProcessor.cpp
    SegmentSingleProcessor2.cpp
    ShapingTypeData.cpp
    SimpleArrayProcessor.cpp
    SimpleArrayProcessor2.cpp
    SinglePositioningSubtables.cpp
    SingleSubstitutionSubtables.cpp
    SingleTableProcessor.cpp
    SingleTableProcessor2.cpp
    StateTableProcessor.cpp
    StateTableProcessor2.cpp
    SubstitutionLookups.cpp
    SubtableProcessor.cpp
    SubtableProcessor2.cpp
    ThaiLayoutEngine.cpp
    ThaiShaping.cpp
    ThaiStateTables.cpp
    TibetanLayoutEngine.cpp
    TibetanReordering.cpp
    TrimmedArrayProcessor.cpp
    TrimmedArrayProcessor2.cpp
    ValueRecords.cpp
    loengine.cpp
)

target_compile_definitions(icule PRIVATE U_LAYOUT_IMPLEMENTATION)

target_link_libraries(icule PUBLIC icuuc)

target_include_directories(
    icule
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/..>
)

install(
    TARGETS icule
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

set_target_properties(icule PROPERTIES EXPORT_NAME le)
