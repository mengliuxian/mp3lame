cmake_minimum_required(VERSION 3.22.1)

project("mp3lame")

# 自动收集 lame 下的所有 cpp 文件
file(GLOB CPP_LIST "lame/*.cpp")

# 自动收集 lame 下的所有 c 文件
file(GLOB C_LIST "lame/*.c")

# 创建库
add_library(mp3lame
        SHARED
        mp3-encoder.c ${CPP_LIST} ${C_LIST})

# 指定头文件目录
target_include_directories(
        mp3lame
        PUBLIC
        lame           # 编译时去 lame 找 .h 文件
)

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        mp3lame
        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})

## 自定义文件输出路径
#set_target_properties(mp3lame PROPERTIES
#        LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}
#        )
