Makefile
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


编译应用程序模板
    - 同级目录创建barcode_reader.c
    - 下面的代码拷贝到Makefile中, 执行make即可

::

    # 定义编译器
    CC		= arm-linux-gnueabi-gcc

    # 编译选项
    CCFLAGS = -Wall -Werror -std=c99 -shared -fPIC 

    # 通配符函数表示目录下所有.c文件,相当于: SRCS = main.c a.c b.c
    SRCS 	= $(wildcard *.c)

    # 通配符函数把列表中的.c全部替换为.o, 相当于: OBJS = main.o a.o b.o
    OBJS	= $(patsubst %c, %o, $(SRCS))

    # 编译头文件路径
    INC		= -I../common \
                    -I../../../../mpp-app/include/mpp/system/include/

    # 可执行文件的名字
    TAG_ELF	= barcode_reader
    TAG_LIB	= barcode_reader.so

    .PHONY:all clean

    all:$(TAG_ELF) $(TAG_LIB)

    # 编译可执行文件
    $(TAG_ELF): $(OBJS)
        @$(CC) -o $@ $^
        @echo LD $^ 
        @echo "\033[32m$@ \033[0m"

    # 编译动态库文件
    $(TAG_LIB):$(OBJS)
        @$(CC) -o $@ $^
        @echo "\033[32m$@ \033[0m"

    # 编译源文件
    %o:%c
        @$(CC) $(INC) $(CCFLAGS) -c $^
        @echo CC $^

    # 清除生成的文件
    clean:
        rm -rf $(OBJS) $(TAG_ELF) $(TAG_LIB)
