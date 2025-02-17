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
        ${SOURCES})

if(WASM)
    target_compile_definitions(${target_name} PRIVATE EMSCRIPTEN_USE_EMBEDDED_GLFW3=1)
endif()

# Define variable for include directories
set(IMGUI_INCLUDE_DIRS 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

# Define variable for link libraries
set(IMGUI_LIBRARIES ImGui glfw OpenGL::GL)

# Export variables
set(IMGUI_INCLUDE_DIRS ${IMGUI_INCLUDE_DIRS} PARENT_SCOPE)
set(IMGUI_LIBRARIES ${IMGUI_LIBRARIES} PARENT_SCOPE)

# Add include directories
target_include_directories(ImGui PUBLIC ${IMGUI_INCLUDE_DIRS})

# Link libraries
target_link_libraries(ImGui PUBLIC glfw OpenGL::GL)