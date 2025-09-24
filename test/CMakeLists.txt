cmake_minimum_required(VERSION 3.18)
project(CSR5_Test LANGUAGES CXX CUDA)

# Add executable
add_executable(spmv_test src/main.cu)

# Include directories
target_include_directories(spmv_test PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../build/include ${CMAKE_CURRENT_SOURCE_DIR}/include)

# Link to the library
target_link_libraries(spmv_test PRIVATE csr5_cuda)

# Set CUDA architectures
set_target_properties(spmv_test PROPERTIES CUDA_ARCHITECTURES "75;80;86;89;90;120")

# Define macros
target_compile_definitions(spmv_test PRIVATE VALUE_TYPE=double NUM_RUN=1000)