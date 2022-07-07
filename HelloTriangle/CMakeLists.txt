project("Hello Triangle")
cmake_minimum_required(VERSION 3.21)

# to fix issues with unicode on VS
add_definitions(-D_UNICODE)
add_definitions(-DUNICODE)

# link everything with direct3d12 libs
link_libraries(
d3d12.lib
dxguid.lib
DXGI.lib
d3dcompiler.lib
)

set(HelloTriangle1_SOURCES
D3D12HelloTriangle.cpp
DXSample.cpp
stdafx.cpp
Win32Application.cpp
)

set(HelloTriangle1_HEADERS
D3D12HelloTriangle.h
DXSample.h
DXSampleHelper.h
stdafx.h
Win32Application.h
)

set(HelloTriangle1_SHADERS
shaders.hlsl
)

# please VS don't try to compile the hlsl file yourself
set_source_files_properties(shaders.hlsl PROPERTIES VS_TOOL_OVERRIDE "None")

# will be needed later
# set_source_files_properties(resources/MeshShader.hlsl PROPERTIES 
#     VS_SHADER_TYPE Mesh
#     VS_SHADER_MODEL 6.5
# )

# --------------------------------------------------- 

add_executable(HelloTriangle1 WIN32 Main.cpp ${HelloTriangle1_HEADERS} ${HelloTriangle1_SOURCES} ${HelloTriangle1_SHADERS})

target_include_directories(HelloTriangle1 PUBLIC ${CMAKE_CURRENT_LIST_DIR})
source_group("Shaders" FILES ${HelloTriangle1_SHADERS})

