project(Example1)

include_directories(
	"${CMAKE_SOURCE_DIR}/core/include"
)

CUDA_ADD_EXECUTABLE(Example1 example1.cu)
TARGET_LINK_LIBRARIES(Example1 FEM_CORE)

CUDA_ADD_EXECUTABLE(Example2 example2.cu)
TARGET_LINK_LIBRARIES(Example2 FEM_CORE)

CUDA_ADD_EXECUTABLE(Example3 example3.cu)
TARGET_LINK_LIBRARIES(Example3 FEM_CORE)
