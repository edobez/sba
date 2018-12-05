cmake_minimum_required(VERSION 3.0)
project(sba)

option(BUILD_SHARED_LIBS "Build shared libs" OFF)
option(USE_MKL "Use Intel MKL for BLAS/LAPACK" OFF)
option(BUILD_DEMO "Compile provided demo" ON)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

# Select source files to build
set(SOURCES src/sba_levmar.c src/sba_levmar_wrap.c
    src/sba_lapack.c src/sba_crsm.c src/sba_chkjac.c)
set(PUBLIC_HEADERS src/sba.h)

# Add targets
# if (BUILD_SHARED_LIBS)
#     add_library(sba SHARED ${SOURCES})
# else()
#     add_library(sba STATIC ${SOURCES}) 
# endif()
add_library(sba STATIC ${SOURCES}) 
target_include_directories(sba PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)

# Link BLAS/LAPACK
if(USE_MKL)
    find_package(MKL REQUIRED)
    target_link_libraries(sba PRIVATE mkl)
else()
    find_package(BLAS REQUIRED)
    find_package(LAPACK REQUIRED)
    target_link_libraries(sba PRIVATE -lm ${BLAS_LIBRARIES} ${LAPACK_LIBRARIES})
endif()

# Define install command
install(TARGETS sba DESTINATION lib)
install(FILES ${PUBLIC_HEADERS} DESTINATION include)

# Compile demo
if(BUILD_DEMO)
    add_subdirectory(demo)
endif()