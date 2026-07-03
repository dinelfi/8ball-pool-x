cmake_minimum_required(VERSION 3.20)
project(8ball-pool-x CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Configuración para DLL
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
add_library(8ball-pool-x SHARED
    src/main.cpp
    src/overlay/overlay.cpp
    src/trajectory/trajectory.cpp
    src/autoplay/autoplay.cpp
    src/hooks/d3d11_hook.cpp
)

# Incluir directorios
target_include_directories(8ball-pool-x PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/deps/imgui
    ${CMAKE_CURRENT_SOURCE_DIR}/deps/imgui/backends
)

# Librerías de Windows
target_link_libraries(8ball-pool-x
    d3d11.lib
    dxgi.lib
    d3dcompiler.lib
    winmm.lib
)

# Flags de compilación
if(MSVC)
    target_compile_options(8ball-pool-x PRIVATE /W4 /WX)
    set_target_properties(8ball-pool-x PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)
endif()

# Output
set_target_properties(8ball-pool-x PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)
