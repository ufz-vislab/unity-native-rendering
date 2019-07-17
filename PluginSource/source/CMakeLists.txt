cmake_minimum_required(VERSION 3.12)

project(UnityNativeRendering)

if(UNIX)
    find_package(OpenGL REQUIRED)
endif()

if(APPLE)
    find_library(FOUNDATION_LIBRARY Foundation REQUIRED)
endif()

add_library(RenderingPlugin SHARED
    RenderAPI_D3D11.cpp
    RenderAPI_D3D12.cpp
    RenderAPI_Metal.mm
    RenderAPI_OpenGLCoreES.cpp
    RenderAPI_Vulkan.cpp
    RenderAPI.cpp
    RenderingPlugin.cpp
)

if(APPLE)
    set_target_properties(RenderingPlugin PROPERTIES
        SUFFIX ".bundle"
        PREFIX ""
    )
    target_link_libraries(RenderingPlugin PUBLIC OpenGL::GL ${FOUNDATION_LIBRARY})
endif()

set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/../../UnityProject/Assets/Plugins)
install(TARGETS RenderingPlugin DESTINATION ".")
