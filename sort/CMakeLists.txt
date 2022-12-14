project(Sort)

# 此处设置目的为练习CMake使用,同时生成动态库与静态库
add_subdirectory(algorithm/bubbleSort)
add_subdirectory(algorithm/heapSort)
add_subdirectory(algorithm/insertSort)
add_subdirectory(algorithm/mergeSort)
add_subdirectory(algorithm/quickSort)
add_subdirectory(algorithm/selectSort)
add_subdirectory(algorithm/shellSort)
add_subdirectory(algorithm/radixSort)

# 需要将动态链接库的路径添加到系统环境变量 Path 里面 / 程序所在目录
# 如果没有设置的话，出现的情况就是exe编译成功，运行的时候不执行任何操作就结束
file(GLOB allDLL "lib/*.dll")
file(COPY ${allDLL} DESTINATION ${PROJECT_SOURCE_DIR}/output)
message("allDLL: ${allDLL}")

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/output)

add_executable(${PROJECT_NAME} testSort.c)

target_link_libraries(${PROJECT_NAME}
PUBLIC
    libbubbleSort
    libheapSort
    libinsertSort
    libmergeSort
    libquickSort
    libselectSort
    libshellSort
    libradixSort
)

target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${PROJECT_SOURCE_DIR}/include/
)

target_link_directories(${PROJECT_NAME}
    PUBLIC
        ${PROJECT_SOURCE_DIR}/lib/
)