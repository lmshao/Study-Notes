# 1. HelloWorld
无头文件

```Makefile
all:Hello
Hello:
    gcc -o hello hello.c
clean:
    rm -rf hello
```

有带头文件

```Makefile
INCLUDE=-I./include/
all:Hello
Hello:
    gcc -o hello hello.c $(INCLUDE)
clean:
    rm -rf hello
```

#2 变量

```Makefile
$@	#目标文件
$^	#所有依赖的文件
$<	#第一个依赖的文件
```

假设有main.c aa.c aa.h bb.c bb.h这5个文件需要编译  
直接编译  
 
```sh
$ gcc -c main.c 
$ gcc -c aa.c 
$ gcc -c bb.c 
$ gcc -o main main.o aa.o bb.o
```


