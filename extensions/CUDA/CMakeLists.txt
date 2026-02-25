cmake_minimum_required(VERSION 3.22)
project(SofaValidation.CUDA LANGUAGES CXX CUDA)

set(HEADER_FILES
    src/SofaValidation/CUDA/init.h
    src/SofaValidation/CUDA/config.h.in
)

set(SOURCE_FILES
    src/SofaValidation/CUDA/init.cpp
    src/SofaValidation/CUDA/CudaExtraMonitor.cpp
)

sofa_find_package(SofaValidation REQUIRED)
sofa_find_package(SofaCUDA REQUIRED)

add_library(${PROJECT_NAME} SHARED ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} SofaValidation)
target_link_libraries(${PROJECT_NAME} SofaCUDA)

sofa_create_package_with_targets(
    PACKAGE_NAME ${PROJECT_NAME}
    PACKAGE_VERSION ${Sofa_VERSION}
    TARGETS ${PROJECT_NAME} AUTO_SET_TARGET_PROPERTIES
    INCLUDE_SOURCE_DIR "src"
    INCLUDE_INSTALL_DIR "${PROJECT_NAME}"
    RELOCATABLE "plugins"
)
