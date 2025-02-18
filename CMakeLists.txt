cmake_minimum_required(VERSION 3.1)
project(ImGui)

# Define source files
set(SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    imgui_tables.cpp
    imgui_demo.cpp
    misc/cpp/imgui_stdlib.cpp
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_opengl3.cpp
)

# Define header files
set(HEADERS
    imgui.h
    imgui_internal.h
    imconfig.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    misc/cpp/imgui_stdlib.h
)

# Add as static library
add_library(ImGui STATIC
        ${HEADERS}
        ${SOURCES}
)

# Add include directories
target_include_directories(ImGui
PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

# Link libraries
target_link_libraries(ImGui
PUBLIC
    glfw
    OpenGL::GL
)

# Export variables
set(IMGUI_LIBRARIES ImGui PARENT_SCOPE)

if(WASM)
    target_compile_definitions(${PROJECT_NAME} PRIVATE EMSCRIPTEN_USE_EMBEDDED_GLFW3=1)
endif()

