cmake_minimum_required(VERSION 3.14)
project(PSHDDTools)

# Include third party libraries
include(third_party/third_party.cmake)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
# Export compile_commands.json
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)
set(BUILD_SHARED_LIBS OFF)

# Change this to turn debug mode on/off
# for the whole project
set(CMAKE_BUILD_TYPE RELEASE)

# O3 for max optimization and -flto for linker optimization 
if (MSVC)
    set(CMAKE_C_FLAGS_RELEASE "-Ox")
else()
    # Static linking for C objects
    set(CMAKE_C_FLAGS "-Wall -static")
    set(CMAKE_C_FLAGS_DEBUG "-g")
    set(CMAKE_C_FLAGS_RELEASE "-O3 -flto")
endif()

# Same flags as for C
if (MSVC)
    set(CMAKE_CXX_FLAGS_RELEASE "-Ox")
else()
    set(CMAKE_CXX_FLAGS_RELEASE "-O3 -flto")
    set(CMAKE_CXX_FLAGS "-Wall -Wextra")
    set(CMAKE_CXX_FLAGS_DEBUG "-g")
endif()

# Include all the executables/libraries
add_subdirectory(core)
add_subdirectory(decrypt-tool)
add_subdirectory(hex-viewer)
add_subdirectory(mount-tool)
add_subdirectory(file-explorer)
add_subdirectory(bindings)
