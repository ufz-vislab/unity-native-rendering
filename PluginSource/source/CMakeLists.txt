cmake_minimum_required(VERSION 3.12)

project(UnityNativeRendering)

add_library(RenderingPlugin
    RenderAPI.cpp
    RenderingPlugin.cpp
)

if(UNIX)
    target_sources(RenderingPlugin PUBLIC RenderAPI_OpenGLCoreES.cpp)
endif()

if(APPLE)
    set_target_properties(RenderingPlugin PROPERTIES SUFFIX ".bundle")
endif()
