add_library(rtmidi
    RtMidi.cpp
    RtMidi.h
)

if (APPLE)
    message(STATUS "Building rtmidi for OSX with CoreMidi.")
    target_compile_definitions(rtmidi PUBLIC "__MACOSX_CORE__")

    find_library(COREAUDIO_LIBRARY CoreAudio)
    find_library(COREFOUNDATION_LIBRARY CoreFoundation)
    find_library(COREMIDI_LIBRARY CoreMidi)

    target_link_libraries(rtmidi
        ${COREAUDIO_LIBRARY}
        ${COREFOUNDATION_LIBRARY}
        ${COREMIDI_LIBRARY}
    )
endif ()

if (MSVC)
    message(STATUS "Building rtmidi for Windows with Windows MM.")
    target_compile_definitions(rtmidi PUBLIC "__WINDOWS_MM__")

    target_link_libraries(rtmidi winmm.lib)
endif ()

target_include_directories(rtmidi
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}
)

set_target_properties(rtmidi PROPERTIES
                      FOLDER "External/rtmidi")