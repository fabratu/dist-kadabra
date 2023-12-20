cmake_minimum_required(VERSION 3.12)
project(dist-kadabra CXX)

find_package(PkgConfig)

pkg_check_modules(NETWORKIT REQUIRED IMPORTED_TARGET networkit)
pkg_check_modules(FABRY REQUIRED IMPORTED_TARGET fabry)

find_package(OpenMP)

add_executable(dist-kadabra main.cpp DistributedKadabra.cpp)
target_include_directories(dist-kadabra PUBLIC "${PROJECT_SOURCE_DIR}/." ${NETWORKIT_INCLUDE_DIRS} ${FABRY_INCLUDE_DIRS})
target_link_libraries(dist-kadabra PUBLIC OpenMP::OpenMP_CXX PkgConfig::NETWORKIT PkgConfig::FABRY)
set_target_properties(dist-kadabra PROPERTIES INSTALL_RPATH "\\\$ORIGIN/lib")
install(TARGETS dist-kadabra DESTINATION ${CMAKE_INSTALL_PREFIX

find_library(CLAMPI_LIBRARY
    NAMES clampi libclampi
    HINTS "${CLAMPI_PREFIX}/lib"
    REQUIRED
)

target_link_libraries(dist-kadabra PUBLIC ${CLAMPI_LIBRARY})
