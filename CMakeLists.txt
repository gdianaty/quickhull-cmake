cmake_minimum_required(VERSION 3.10)
project(QuickHullLib)

# Collect all source files
set(SOURCES
    QuickHull.cpp
)

# Collect all header files (for IDEs and install, not strictly needed for build)
set(HEADERS
    include/QuickHull.hpp
    include/MathUtils.hpp
    include/HalfEdgeMesh.hpp
    include/ConvexHull.hpp
    include/Structs/Mesh.hpp
    include/Structs/Plane.hpp
    include/Structs/Pool.hpp
    include/Structs/Ray.hpp
    include/Structs/Vector3.hpp
    include/Structs/VertexDataSource.hpp
)

add_library(quickhull STATIC ${SOURCES} ${HEADERS})

target_include_directories(quickhull PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include/Structs
)

# Optionally, set C++ standard
set_target_properties(quickhull PROPERTIES CXX_STANDARD 11 CXX_STANDARD_REQUIRED YES)

# Install rules
install(TARGETS quickhull
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)

# Install public headers (preserving directory structure)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
        DESTINATION include
        FILES_MATCHING PATTERN "*.hpp")
