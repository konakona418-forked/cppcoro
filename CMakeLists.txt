cmake_minimum_required(VERSION 3.15)
project(cppcoro LANGUAGES CXX)

add_library(cppcoro)

file(GLOB CPPORO_SOURCES
     ${CMAKE_CURRENT_SOURCE_DIR}/lib
     "lib/*.cpp" "lib/*.hpp"
    )
target_sources(cppcoro PRIVATE ${CPPORO_SOURCES})

target_include_directories(cppcoro PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

target_compile_features(cppcoro PUBLIC cxx_std_20)
# target_compile_options(cppcoro PUBLIC "-std=c++20")

include(GNUInstallDirs)
install(TARGETS cppcoro
    EXPORT cppcoroTargets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

install(DIRECTORY include/cppcoro/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/cppcoro
)

message(STATUS "[cppcoro] Configured cppcoro library target")
