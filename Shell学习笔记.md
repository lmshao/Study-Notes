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
##grep
##sed
##wc
##

#3 Shell语法