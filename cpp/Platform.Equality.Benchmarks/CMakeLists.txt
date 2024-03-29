cmake_minimum_required(VERSION 3.8)
project(Platform.Equality)

include_directories(../Platform.Equality)

include(FetchContent)

FetchContent_Declare(
        benchmark
        URL https://github.com/google/benchmark/archive/refs/tags/v1.5.3.zip
)

FetchContent_MakeAvailable(benchmark)
FetchContent_GetProperties(benchmark)
if(NOT benchmark_POPULATED)
    FetchContent_Populate(benchmark)
    add_subdirectory(${benchmark_SOURCE_DIR} ${benchmark_BINARY_DIR})
endif()

file(GLOB EXECUTABLE_FILES *.cpp)
message(${EXECUTABLE_FILES})

add_executable(Platform.Equality.Benchmarks Main.cpp)
set_target_properties(Platform.Equality.Benchmarks PROPERTIES CXX_STANDARD 20)
target_link_libraries(Platform.Equality.Benchmarks PUBLIC benchmark benchmark_main)
