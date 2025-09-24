cmake_minimum_required(VERSION 3.18)

# Set install prefix
set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE PATH "Installation directory")

project(CSR5_CUDA VERSION 1.0.0 LANGUAGES C CXX CUDA)

# Find CUDA
find_package(CUDA REQUIRED)

# Set CUDA architectures
set(CMAKE_CUDA_ARCHITECTURES 75 80 86 89 90 120)

# Option to build test
option(BUILD_TEST "Build the test executable" ON)

# Add subdirectories
add_subdirectory(src)

if(BUILD_TEST)
    add_subdirectory(test)
endif()

# Install the library
install(TARGETS csr5_cuda
    EXPORT csr5_cudaTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

# Install headers
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
    DESTINATION include
)

# Install export
install(EXPORT csr5_cudaTargets
    FILE csr5_cudaTargets.cmake
    NAMESPACE csr5_cuda::
    DESTINATION lib/cmake/csr5_cuda
)

# Create config file
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/csr5_cudaConfigVersion.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion
)

configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/csr5_cudaConfig.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/csr5_cudaConfig.cmake"
    INSTALL_DESTINATION lib/cmake/csr5_cuda
)

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/csr5_cudaConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/csr5_cudaConfigVersion.cmake"
    DESTINATION lib/cmake/csr5_cuda
)