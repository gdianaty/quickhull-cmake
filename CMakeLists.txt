cmake_minimum_required(VERSION 3.10)
project(QuickHullLib)

# Collect all source files
set(SOURCES
    QuickHull.cpp
)

# Collect all header files (for IDEs and install, not strictly needed for build)
set(HEADERS
    QuickHull.hpp
    MathUtils.hpp
    HalfEdgeMesh.hpp
    ConvexHull.hpp
    Structs/Mesh.hpp
    Structs/Plane.hpp
    Structs/Pool.hpp
    Structs/Ray.hpp
    Structs/Vector3.hpp
    Structs/VertexDataSource.hpp
)

add_library(quickhull STATIC ${SOURCES} ${HEADERS})

target_include_directories(quickhull PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/Structs
)

# Optionally, set C++ standard
set_target_properties(quickhull PROPERTIES CXX_STANDARD 11 CXX_STANDARD_REQUIRED YES)
