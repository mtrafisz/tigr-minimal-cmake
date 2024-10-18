cmake_minimum_required (VERSION 3.20)
project (tigr)

file(GLOB_RECURSE SOURCES "tigr.c" "tigr.h")
add_library(${PROJECT_NAME} ${SOURCES})

if (WIN32)
    find_package(OpenGL REQUIRED)
    find_library(GDI32_LIBRARY gdi32)

    target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES} ${GDI32_LIBRARY})
elseif (UNIX)
    find_package(OpenGL REQUIRED)
    find_library(GLU_LIBRARY GLU)
    find_library(X11_LIBRARY X11)

    target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES} ${GLU_LIBRARY} ${X11_LIBRARY})
elseif (APPLE)
    find_library(COCOA_LIBRARY Cocoa)
    find_library(OPENGL_LIBRARY OpenGL)

    target_link_libraries(${PROJECT_NAME} ${COCOA_LIBRARY} ${OPENGL_LIBRARY})
endif()
