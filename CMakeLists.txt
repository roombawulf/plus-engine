cmake_minimum_required(VERSION 3.0...3.26)
project(
    Plus-Engine # name of project
    VERSION 0.1.0 # version number
    LANGUAGES CXX C # languages used
)

function(target_treat_all_warnings_as_errors Target)
    # Treat warnings as errors
    set_target_properties(${Target} PROPERTIES COMPILE_WARNING_AS_ERROR ON)

    # Turn all warnings on
    if (MSVC)
        target_compile_options(${Target} PRIVATE /W4)
    else()
        target_compile_options(${Target} PRIVATE -Wall -Wextra -pedantic)
    endif()
endfunction()

# add packages
add_subdirectory(glfw)
add_subdirectory(webgpu)
add_subdirectory(glfw3webgpu)


add_executable(App main.cpp)

#link libraries
target_link_libraries(App PRIVATE glfw webgpu glfw3webgpu)

set_target_properties(App PROPERTIES CXX_STANDARD 17)
target_treat_all_warnings_as_errors(App)
target_copy_webgpu_binaries(App)

