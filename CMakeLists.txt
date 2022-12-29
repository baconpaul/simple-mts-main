cmake_minimum_required(VERSION 3.10)

set(CMAKE_OSX_DEPLOYMENT_TARGET 10.11 CACHE STRING "Build for 10.11")

project(simple-mts-main VERSION 0.9.0 LANGUAGES CXX)

add_subdirectory(libs/JUCE)
add_subdirectory(libs/tuning-library)
add_subdirectory(libs/oddsound-mts)
add_subdirectory(libs/clap-juce-extensions)

juce_add_plugin(${PROJECT_NAME}
    PRODUCT_NAME "Simple MTS Main"
    COMPANY_NAME "Surge Synth Team"  
    BUNDLE_ID "org.surge-synth-team.simple-mts-main"
    PLUGIN_MANUFACTURER_CODE VmbA
    PLUGIN_CODE SmtM

    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MIDI_EFFECT FALSE
    
    FORMATS AU VST3 Standalone
)

clap_juce_extensions_plugin(TARGET ${PROJECT_NAME}
        CLAP_ID "org.surge-synth-team.simple-mts-main"
        CLAP_FEATURES instrument)

target_include_directories(${PROJECT_NAME}
  PRIVATE
  src/
)

target_sources(${PROJECT_NAME} PRIVATE src/PluginEditor.cpp src/PluginProcessor.cpp)

target_compile_definitions(${PROJECT_NAME} PUBLIC
    JUCE_ALLOW_STATIC_NULL_VARIABLES=0
    JUCE_STRICT_REFCOUNTEDPOINTER=1

    JUCE_VST3_CAN_REPLACE_VST2=0
    JUCE_USE_CURL=0
    JUCE_WEB_BROWSER=0

    JUCE_DISPLAY_SPLASH_SCREEN=0
    JUCE_REPORT_APP_USAGE=0

    JUCE_ALSA=0
    JUCE_JACK=0
)

target_link_libraries(${PROJECT_NAME} PUBLIC
        juce::juce_graphics
        juce::juce_audio_processors
        juce::juce_audio_utils
        juce::juce_audio_devices
        tuning-library
        )

