# 1. HelloWorld
无头文件

```makefile
all:Hello
Hello:
    gcc -o hello hello.c
clean:
    rm -rf hello
```

有带头文件

```makefile
INCLUDE=-I./include/
all:Hello
Hello:
    gcc -o hello hello.c $(INCLUDE)
clean:
    rm -rf hello
```

#2 变量

##2.1 $@$^ $<

- $@&emsp;&emsp;目标文件
- $^&emsp;&emsp;所有依赖的文件
- $<&emsp;&emsp;第一个依赖的文件

假设有main.c aa.c aa.h bb.c bb.h这5个文件需要编译  
直接编译  
 
```sh
$ gcc -c main.c 
$ gcc -c aa.c 
$ gcc -c bb.c 
$ gcc -o main main.o aa.o bb.o
```

可以把上述命令写入makefile

```makefile
main: main.o aa.o bb.o 
	gcc -o main main.o aa.o bb.o 

main.o: main.c aa.h bb.h 
	gcc -c main.c 

aa.o: aa.c aa.h 
	gcc -c aa.c 

bb.o: bb.c bb.h
	gcc -c bb.c
```



使用者3个变量重写示例makefile

```makefile
main: main.o aa.o bb.o 
	gcc -o $@ $^ 

main.o：main.c aa.h bb.h 
	gcc -c $< 

aa.o: aa.c aa.h 
	gcc -c $< 

bb.o: bb.c bb.h 
	gcc -c $< 
```

使用缺省规则```.c.o:```所有.o文件依赖相应.c文件  

```makefile
main: main.o aa.o bb.o 
	gcc -o $@ $^ 

.c.o:
	gcc -c $< 
```

##2.2 wildcard patsubst

在变量的定义和函数引用时，通配符将失效。这种情况下如果需要通配符有效，就需要使用函数“wildcard”  

```makefile
SRC := $(wildcard *.c)		#获取当前目录下所有.c文件

OBJ := $(patsubst %.c,%.o,$(SRC) )	#把SRC后缀.c替换为.o
OBJ := $(SRC:%.c=%.o)				#把SRC后缀.c替换为.o

```

##2.3 = ：= ？= +=

- =&emsp;&emsp;是最基本的赋值
- :=&emsp;&emsp;是覆盖之前的值
- ?=&emsp;&emsp;是如果没有被赋值过就赋予等号后面的值
- +=&emsp;&emsp;是添加等号后面的值

示例
```makefile
x = abc
y = ur$(x)
x = xyz
```
最后结果：x为xyz，y为urxyz.

```make
x := abc
y := ur$(x)
x := xyz
```
最后结果：x为xyz，y为urabc.  
  
= 搜索到最后再赋值  
:=  当前位置直接赋值  


## 3 示例

有文件：main.cpp RTSP.h RTSP.cpp

```makefile
Dawn_RTSP_Server:main.o RTSP.o
	g++ -o $@ $^
.c.o:
	g++ -c $<
    
clean:
	rm -f *.o Dawn_RTSP_Server
```

或者

```makefile
Dawn_RTSP_Server:main.o RTSP.o
	g++ -o $@ $^
%o:%c
	g++ -c $<
    
clean:
	rm -f *.o Dawn_RTSP_Server
```

或者   
```make
Dawn_RTSP_Server:main.o RTSP.o
	g++ -o $@ $^
main.o:main.cpp RTSP.h
	g++ -c $^
RTSP.o:RTSP.cpp RTSP.h
	g++ -c $^
```

