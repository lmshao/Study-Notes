#1 正则表达式
##1.1 简单正则表达式

表达式 | 匹配
|:---:|:---|
^tolstoy | 以tolstoy开始的一行
tolstoy$ | 以tolstoy结尾的一行
^tolstoy$ | 只有tolstoy的一行
[Tt]olstoy | 任意位置含有Tolstoy或tolstoy的一行
tol.toy | tol和toy中间有一个字符的一行
tol.*toy | tol和toy中间有多个或0个字符的一行

##1.2 方括号表达式

POSIX字符集  

类别 | 匹配字符
|:---:|:---|
[:alnum:] | 数字
[:digit:] | 数字
[:alpha:] | 字母
[:lower:] | 小写字母
[:upper:] | 大写字母
[:blank:] | 空格与Tab
[:graph:] | 非空格字符
[:cntrl:] | 控制字符
[:punct:] | 标点符号
[:print:] | 可显示的字符
[:xdigit:] | 十六进制数字

##1.3 基本正则表达式
###后向引用



#2 常用命令
##2.1 grep

```sh
$ grep -G		#BRE表达式  
$ grep -E		#ERE表达式  
$ grep -i		#不区别大小写字母  
$ grep -v		#排除匹配
```

##2.2 cut

```sh
$ cut -b 3		#提取每一行的第3个字节
$ cut -b 3-5,8	#提取每一行的第3-5&8个字节
$ cut -b -3		#提取每一行的第3字节和之前所有
$ cut -b 3-		#提取每一行的第3个字节和之后所有
$ cut -c 3		#提取第3个字符
$ cut -f 2		#以TAB为分隔符取第2个域
$ cut -d : -f 2	#以冒号为分隔符取第2个域
```

##2.3 wc

```sh
$ wc	#行数+单词数+字节数+文件名 
$ wc -l	#行数
$ wc -c	#字节数
$ wc -w	#字数
```

##2.4 sed
可以单引号或双引号  
###2.4.1 不显示某行（删除某行,不写入文件） d

```sh
$ sed '1d' file.txt		#不显示第一行
$ sed '$d' file.txt		#不显示最后一行
$ sed '1,3d' file.txt	#不显示1-3行
$ sed '3,$d' file.txt	#不显示第3到最后一行
$ sed '/abc/d'	file.txt	#不显示abc所在的行
```

###2.4.2 显示某行 p

```sh
$ sed -n '1p' file.txt	#显示第一行
$ sed -n '$p' file.txt	#显示最后一行
$ sed -n '/abc/p'	file.txt	#显示abc所在的行
```

###2.4.3 模式匹配查询

```sh
$ sed -n '/abc/p' file.txt	#显示关键字abc所在的行
$ sed -n '/\$/p' file.txt	#显示关键字$所在行，使用\屏蔽特殊含义 
```

###2.4.4 增加一行或多行字符 a

```sh
$ sed '1a love u' file.txt		#在第一行后增加一行“love u”
$ sed '1a \ ' file.txt			#在第一行后增加一空行（其实是增加空格，\转义）
$ sed '1a love u\nlove me' file.txt		#在第一行后增加两行
$ sed '1,3a love u' file.txt	#在第1-3行后各增加一行“love u”

```

###2.4.5 替换某行 c

```sh
$ sed '1c love' file.txt	#把第一行替换为love
$ sed '1,2c love' file.txt	#把1-2行都替换为love

```

###2.4.6 替换与删除某行 s

```
$ sed 's/abc/xyz/g' file.txt	#把abc替换为xyz
$ sed 's/abc//g'				#删除abc

```

###2.4.7 直接写入文件，不能用管道 -i
可以使用以上的各操作  

```sh
$ sed -i '1a bye' file.txt	#在最后一行后插入“bye”
$
$ sed -i '$d' file.txt		#删除最后一行
$
$ sed -i '/abc/d' file.txt	#删除abc所在的行
```

##2.5 sort

##2.6 awk

输出以空格分割的第一部分字符，并加上.jpg作为后缀

```sh
md5sum $file | awk '{print $1".jpg"}'
```

#3 Shell语法

##3.1 if

语句格式  

```sh
if Condition
then
	Command
elif Condition2
	Command
else
	Command
fi
```

条件表达式  

```sh
if [ -f file ]	#文件存在
if [ -d doc ]		#目录存在
if [ -r file ]	#可读
if [ -w file ]	#可写
if [ -x file ]	#可执行

#数值比较
if [int1 -eq int2]	#int1 == int2
if [int1 -ne int2]	#int1 != int2
if [int1 -ge int2]	#int1 >= int2
if [int1 -gt int2]	#int1 >  int2
if [int1 -le int2]	#int1 <= int2
if [int1 -lt int2]	#int1 <  int2

#字符串比较
if [$str1 = $str2]	#str1 == str2
if [$str1 != $str2]	#str1 != str2
if [-n $str]		#str非空
if [-z $str]		#str为空
if [$str]			#str非空

#逻辑表达式
[! expression]		#取反
[ex1 -a ex2]		#与
[ex1] && [ex2]		#与
[ex1 -o ex2]		#或
[ex1] || [ex2] 		#或
```


##3.2 for

##3.3 while