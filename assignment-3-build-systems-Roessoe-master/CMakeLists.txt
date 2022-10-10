cmake_minimum_required(VERSION 3.22.1)
project(assignment-3-build-systems-Roessoe-master VERSION 0.1.0)

add_executable(lift_sim)

target_sources( lift_sim
        PRIVATE
        ./src/buttons.cpp
        ./src/lift.cpp
        ./src/lift_down_state.cpp
        ./src/lift_init_state.cpp
        ./src/lift_state.cpp
        ./src/lift_steady_state.cpp
        ./src/lift_up_state.cpp
        main.cpp
        )

include_directories(./inc)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang" OR "${CMAKE_CXX_COMPILER_ID}" MATCHES "GNU")
    set(CXX_GNU_COMPATIBLE ON)
else()
    set(CXX_GNU_COMPATIBLE OFF)
endif()



if ("${CMAKE_CXX_COMPILER_ID}" MATCHES "GNU")
    if ("NOT ${CMAKE_BUILD_TYPE}" MATCHES "Debug" AND " NOT ${CMAKE_BUILD_TYPE}" MATCHES "Release")
        message(FATAL_ERROR "ERROR")
    else("${CMAKE_BUILD_TYPE}" MATCHES "")
        set(CMAKE_BUILD_TYPE "Debug")
    endif ()
endif ()

if(CXX_GNU_LIKE)
    target_compile_options(lift_sim PRIVATE
            # set warnings for all build types
            $<$<CXX_COMPILER_ID:GNU,Clang,AppleClang>:-Wall -Wextra -Wpedantic -Werror -fno-omit-frame-pointer>
            # debug optimisation in Debug
            $<$<AND:$<CXX_COMPILER_ID:GNU,Clang,AppleClang>,$<CONFIG:Release>>:-O3>
            # O3 optimisation Release
            $<$<AND:$<CXX_COMPILER_ID:GNU,Clang,AppleClang>,$<CONFIG:Debug>>:-Og -g>
            )
endif()

# Set options for MSVC
target_compile_options(lift_sim PRIVATE
        # set warnings for all build types
        $<$<CXX_COMPILER_ID:MSVC>:/Wall>
        # debug optimisation in Debug
        $<$<AND:$<CXX_COMPILER_ID:MSVC>,$<CONFIG:Release>>:/O2>
        # O3 optimisation in Release
        $<$<AND:$<CXX_COMPILER_ID:MSVC>,$<CONFIG:Debug>>:/RTC1 /Od /Zi>
        )





