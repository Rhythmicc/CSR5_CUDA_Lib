cmake_minimum_required(VERSION 3.18)
project(CSR5_Lib LANGUAGES C CXX CUDA)

# Define the library
add_library(csr5_cuda STATIC csr5_cuda.cu)

# Include directories
target_include_directories(csr5_cuda PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
    $<INSTALL_INTERFACE:include>
)

# Add mmio as a separate library
# add_library(mmio STATIC mmio.c)
# target_include_directories(mmio PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>)

# Link mmio to csr5_cuda
# target_link_libraries(csr5_cuda INTERFACE mmio)