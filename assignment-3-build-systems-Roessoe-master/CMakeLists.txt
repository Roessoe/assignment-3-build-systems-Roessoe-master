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
        )

include_directories(./inc)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)


