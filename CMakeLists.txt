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

# vcpkg install target
#if (DEFINED CMAKE_TOOLCHAIN_FILE AND CMAKE_TOOLCHAIN_FILE MATCHES "vcpkg")
    include(GNUInstallDirs)
    install(EXPORT quickhullTargets
        FILE quickhullTargets.cmake
        NAMESPACE quickhull::
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/quickhull)
    include(CMakePackageConfigHelpers)
    configure_package_config_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/cmake/quickhullConfig.cmake.in
        ${CMAKE_CURRENT_BINARY_DIR}/quickhullConfig.cmake
        INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/quickhull
    )
    install(FILES ${CMAKE_CURRENT_BINARY_DIR}/quickhullConfig.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/quickhull)
#endif()
