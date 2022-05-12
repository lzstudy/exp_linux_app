CMakeLists.txt
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

编译应用程序模板
    - 同级目录创建barcode_reader.c
    - 下面的代码拷贝到CMakeLists.txt
    - 创建build目录, 执行cmake ..

::

    #工程根目录(即为CMakeLists.txt文件所在目录)
    #message("PROJECT_SOURCE_DIR : " ${PROJECT_SOURCE_DIR})

    #编译目录(即为执行cmake的目录)
    #message("PROJECT_BINARY_DIR : " ${PROJECT_BINARY_DIR})

    #指定最低版本
    cmake_minimum_required(VERSION 3.10)
    
    #指定工程名称
    project(barcode_reader)

    # 设置编译选项
    set(CMAKE_C_COMPILER "arm-linux-gnueabi-gcc")

    # 设置编译选项
    add_compile_options(-std=c11 -Wall)
    add_compile_options(-Werror)

    # 添加源文件
    set(srcs ${PROJECT_SOURCE_DIR}/barcode_reader.c)

    # 添加库路径
    #set(libs ${PROJECT_SOURCE_DIR}/../../../../mpp-app/libs/liblog.so)
    set(libs pthread)

    # 添加头文件路径
    include_directories(${PROJECT_SOURCE_DIR})
    include_directories(${PROJECT_SOURCE_DIR}/../common)
    include_directories(${PROJECT_SOURCE_DIR}/../../../../mpp-app/include/mpp/system/include)
    
    # 生成可执行文件
    add_executable(main ${srcs})
    target_link_libraries(main ${libs})

    # 生成动态库
    add_library(barcode_reader SHARED ${srcs})
    target_link_libraries(barcode_reader ${libs})
