# find_package(CUDA QUIET)
# set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
# set(CMAKE_CXX_FLAGS "-O3 ${CMAKE_CXX_FLAGS}")
# set(CMAKE_CXX_FLAGS "-shared ${CMAKE_CXX_FLAGS}")
# set(CMAKE_CXX_FLAGS "-fPIC ${CMAKE_CXX_FLAGS}")
# set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};--expt-relaxed-constexpr)
# SET(CUDA_PROPAGATE_HOST_FLAGS ON)

# find_program(_nvidia_smi "nvidia-smi")
# if (_nvidia_smi)
#   add_definitions(-DUSE_GPU)
#   message("Compiling GPU-compatible custom operator!")
#   cuda_add_library(SinkhornKnopp SHARED SinkhornKnopp.cpp ../src/sinkhorn.cpp SinkhornKnopp.cu)
# else()
# GPU version is not implemented yet
  add_library(SinkhornKnopp SHARED ../src/sinkhorn.cpp  SinkhornKnopp.cpp)
# endif()

set_property(TARGET SinkhornKnopp PROPERTY POSITION_INDEPENDENT_CODE ON)
target_link_libraries(SinkhornKnopp ${TF_LIB_FILE} )

file(MAKE_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/build)
set_target_properties(SinkhornKnopp PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/build)
