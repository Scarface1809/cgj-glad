cmake_minimum_required(VERSION 3.20.0)
project(glad)

option(GLAD_INSTALL "Generate the install target" ON)

add_library(glad src/gl.c)
target_include_directories(glad
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include/glad>
)

if(GLAD_INSTALL)
    include(GNUInstallDirs)

    install(TARGETS glad
        EXPORT glad-targets
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    )

    install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/glad)

    install(EXPORT glad-targets
        FILE glad-config.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/glad
    )
endif()
