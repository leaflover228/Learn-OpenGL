find_package(OpenGL REQUIRED)

file(GLOB_RECURSE PROJECT_SOURCES "src/*.cpp" "src/*.c" "src/*.cc" "src/*.cxx")

add_executable(lesson1 ${PROJECT_SOURCES})

target_include_directories(lesson1 PRIVATE
    "${GLEW_INCLUDE_DIR}"
    "${GLFW_INCLUDE_DIR}"
    "${PROJECT_SOURCE_DIR}/include"
)

target_compile_definitions(lesson1 PRIVATE ${GLEW_DEFINITIONS})

target_link_libraries(lesson1 PRIVATE
    "${GLEW_LIB}"
    "${GLFW_LIB}"
    OpenGL::GL
)

if(NOT USE_STATIC_GLEW)
    add_custom_command(TARGET lesson1 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different "${GLEW_DLL}" "$<TARGET_FILE_DIR:lesson1>"
    )
endif()

if(NOT USE_STATIC_GLFW)
    add_custom_command(TARGET lesson1 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different "${GLFW_DLL}" "$<TARGET_FILE_DIR:lesson1>"
    )
endif()