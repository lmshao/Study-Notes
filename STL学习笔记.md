#Vector

头文件： ```#include <vector>```

##多维数组初始化

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
