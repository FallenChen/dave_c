cmake_minimum_required(VERSION 3.17)
project(Dave_C C)

set(CMAKE_C_STANDARD 11)

# if compiler is Clang, link libc++, otherwise, link default libstdc++
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -stdlib=libc++ -lc++abi")
endif()

# 遍历项目根目录下所有的 .cpp 文件
file (GLOB_RECURSE files src/*.c)
foreach (file ${files})
    string(REGEX REPLACE ".+/(.+)\\..*" "\\1" exe ${file})
    add_executable (${exe} ${file})
    message (\ \ \ \ --\ src/${exe}.c\ will\ be\ compiled\ to\ bin/${exe})
endforeach ()