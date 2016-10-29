> 在STL基础上加上C++比C多的string等部分

#1. 字符串 String
```#include <string>```

##1.1 迭代器

```cpp
str.begin()			//第一个元素迭代器
str.end()			//最后一个字符的下一位的迭代器
str.rbegin()		//最后一个字符的反向迭代器
str.rend()			//第一个字符的前面的反向迭代器
```

#1.2 元素的访问

```cpp
str.at(2)			//返回第3个字符，同str[2]
str.front()			//返回第一个元素	C++11
str.back()			//返回最后一个元素	C++11
str.c_str()			//返回char *风格字符串
```

##1.3 容量   
   
```cpp
str.length()		//返回字符数量，不包含最后的'\0'
str.size()			//返回字符数量

str.empty()			//检查字符串是否为空 
```

##1.4 操作
### 1.4.1 删除

```cpp
str.clear()			//删除全部内容

str.erase(2,3);		//删除str[2]连续的3个字符
str.erase(2);		//删除str[2]及以后的所有字符，保留前面2个

str.erase(str.begin()+1,str.begin()+3);
					//删除这两个迭代器区间的字符
str.erase(str.begin()+3);
					//删除这个迭代器所在的一个字符
```

###1.4.2 插入

```cpp
str.insert(1,4,'x');			//在str[1]位置插入4个‘x’字符
str.insert(1, "abc");			//在str[1]位置插入字符串“abc”
str.insert(1, "abcdefg",4);		//在str[1]位置插入字符串“abcdefg”的前4个字符
str.insert(str.begin()+1,'x');	//在指定迭代器位置插入字符‘x’	C++11
str.insert(str.begin()+1,3,'x');//在指定迭代器位置插入3个字符‘x’	C++11
str.insert(str.begin()+1,  str1.begin(), str1.begin()+4);
								//在指定迭代器位置插入，另一个字符串[first, last)区间的字符
str.push_back('x');		//字符串末尾插入一个字符‘x’
str.pop_back();			//删除最后一个字符

str.append(3, 'x');				//最后插入3个字符‘x’
str.append("abcdefg");			//最后插入字符串“abcdefg”
str.append("abcdefg", 2,4);		//最后插入字符串的第3个开始的连续4个字符
str.append(str1.begin()+1, str1.begin()+4);
								//最后插入另一个字符串[first, last)区间的字符
str.operator+=(str1);			//str后面拼接str1
str.operator+=('x');			//str后面拼接字符‘x’


```

###1.4.3 比较

```cpp
str.compare()
```

###1.4.4 截取

```cpp
str.substr(5)			//截取str[5]和之后的所有字符
str.substr(5， 3)		//截取str[5]之后3个字符

```

###1.4.5 替换

```cpp
str.replace(3， 5， "abc")			//把str[3]开始的5个字符替换为“abc”
str.replace(str.begin()+1, str.begin() + 3, 3, 'A');
									//把迭代器区间的字符替换为3个‘A’
str.replace(str.begin()+1, str.begin() + 3, "abcdefg");
									//把迭代器区间的字符替换为“abcdefg”
str.replace(str.begin()+1, str.begin() + 3, str1.begin(), str1.end());
									//把迭代器区间的字符替换为另一个字符串的迭代器区间的字符
```

###1.4.6 搜索

```cpp
string str = "abcdefg higklmnfg";
str.find("fg");					//返回第一个匹配的f的下标5，若查找不到返回string::npos
str.find("fg"， 4);				//从下标4开始寻找
str.find('f');					//返回第一个字符‘f’的下标

```

###1.4.7 示例
有如下的字符串，需要把“w/cpp”替换为“x/cxx”
```cpp
string str = "http://zh.cppreference.com/w/cpp/string/basic_string/replace";

int i = str.find("com/")+4;		//定位 'w'

//方法一
str.replace(i, 5, "x/cxx");		//把‘w’及后面的5个字符替换为“x/cxx”

//方法二
int	j = str.find("/string");	//定位 '/'

str.replace(str.begin()+i, str.begin()+j,"c/cxx");	//把迭代器区间的字符替换为“x/cxx”

//输出结果 str=http://zh.cppreference.com/x/cxx/string/basic_string/replace

```

#2. 容器 Container
##2.1 Vector

头文件： ```#include <vector>```   
部数据结构：数组。   
随机访问每个元素，所需要的时间为常量。   
在末尾增加或删除元素所需时间与元素数目无关，在中间或开头增加或删除元素所需时间随元素数目呈线性变化。

###二维数组初始化

array[5][2]={0,1,2,3,4,5,6,7,8,9};  
通过一个一维数组给二维数组赋值：  

```cpp
vector<int> tmp;
vector<vector<int> > array;
for(int i=0; i<5; i++)
{
	for(int j=0; j<2;j++)
	{
		tmp.push_back(2*i+j);
	}
	array.push_back(tmp);
	tmp.erase(tmp.begin(), tmp.end());

}

for(int i=0; i<5; i++)
{
	for(int j=0; j<2;j++)
	{
		cout << array[i][j] << " ";
	}
}
```

c++11 有如下方法

```cpp
vector<vector<int> > array = {{0,1}, {2,3}, {4,5}, {6,7}, {8,9}};
```
###反转数组

```cpp
vector<int> vec, revec;
vector<int>::reverse_iterator riter;
for(riter = vec.rbegin();riter!=vec.rend();riter++)
{
	revec.push_back(*riter);
}
```

##2.2 Deque

内部数据结构：数组。   
随机访问每个元素，所需要的时间为常量。   
在开头和末尾增加元素所需时间与元素数目无关，在中间增加或删除元素所需时间随元素数目呈线性变化。   


##2.3 List

内部数据结构：双向环状链表。   
不能随机访问一个元素,可双向遍历。   
在开头、末尾和中间任何地方增加或删除元素所需时间都为常量。   


##2.4 Slist

内部数据结构：单向链表。   
不可双向遍历，只能从前到后地遍历。   
其它的特性同list相似。   


##2.5 Stack

适配器，它可以将任意类型的序列容器转换为一个堆栈，一般使用deque作为支持的序列容器。   
元素只能后进先出（LIFO），不能遍历整个stack。   


##2.6 Queue

适配器，它可以将任意类型的序列容器转换为一个队列，一般使用deque作为支持的序列容器。   
元素只能先进先出（FIFO）。   


##2.7 Set

按照键进行排序存储， 值必须可以进行比较， 可以理解为set就是键和值相等的map。   
键唯一，元素默认按升序排列。   

##2.8 Map

键唯一，元素默认按键的升序排列。   

##2.9 Hash_set

与set相比较，它里面的元素不一定是经过排序的，而是按照所用的Hash函数分派的，它能提供更快的搜索速度（当然跟hash函数有关）。hash_set将key进行hash， 然后将key放在hash值对应的桶中， 原理可以这样理解， hash_set就是key， value相等的hash_map。

##2.10 Hash_map

与map相比较，它里面的元素不一定是按键值排序的，而是按照所用的hash函数分派的，它能提供更快的搜索速度（当然也跟hash函数有关）。   
其它特点与map相同。

#3. 算法 Algorithm
