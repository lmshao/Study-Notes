#分析程序运行结果
## 1. 继承多态
```cpp
class A{  
public:  
    void virtual f()  
    {  
        cout<<"A"<<endl;  
    }  
};  
  
  
class B:public A{  
public:  
    void virtual f()  
    {  
        cout<<"B"<<endl;  
    }  
};  
int main()  
{  
    A* pa=new A();  
    pa->f();  
    B* pb=(B *)pa;  
    pb->f();  
  
    delete pa,pb;  
    pa=new B();  
    pa->f();  
    pb=(B *)pa;  
    pb->f();  
  
    return 0;  
}  
```

运行结果： A A B B.注意虚函数，属于覆盖。

## 2. 继承多态

```cpp
class A {
	void foo()
	{
		cout << "A foo" << endl;
	};
	virtual void bar()
	{
		cout << "A bar" << endl;
	}
};

class B:public A{
	void foo()
	{
		cout << "B foo" << endl;
	};
	virtual void bar()
	{
		cout << "B bar" << endl;
	}
};
int main()
{
	B *b = new B;
	A *a=b;
	a->foo();
	a->bar();
}
```
输出为：   
A foo ； B bar；   
多态要看父类方法是否被重写，有virtual被重写，没有virtual，不会被重写。   

## 3. 继承

```cpp
class A{  
  
public:  
    void  fA()  
    {  
        cout<<"fA()"<<endl;  
  
    }  
};  
  
  
class B:private A{  
  
public:  
    void fB()  
    {  
        fA();  
    }  
  
};  
int main()  
{  
    B b;  
    b.fB(); 	//正确
    b.fA();		//错误
  
    return 0;  
} 
```
b.fB()有输出，b.fA()出错。因为private从A继承，外部不可访问。

## 4. 虚函数表

```cpp
class A
{ 
	virtual void g() 
	{ 
		cout << "A::g" << endl; 
	}

private: 
	virtual void f() 
	{ 
		cout << "A::f" << endl; 
	}
};

class B : public A 
{ 
	void g() 
	{ 
		cout << "B::g" << endl; 
	} 

	virtual void h() 
	{ 
		cout << "B::h" << endl;
	} 
};

typedef void( *Fun )( void );

int main(int argc, char* argv[])
{
	B b; 
	Fun pFun; 
	for(int i = 0 ; i < 3; i++) 
	{ 
		pFun = ( Fun )*( ( int* ) * ( int* )( &b ) + i ); 
		pFun(); 
	}
	return 0;
}
```
输出结果：   
B::g    
A::f    
B::h   

类中如果含有虚函数的话就会有一个隐藏的指针，叫做虚函数指针表头指针（后面用p代替），该指针指向了一个虚函数指针表，该表中存储了类中所有虚函数的地址，其存储顺序就是类中虚函数声明的顺序；    
首先B继承自A，就含有了两个虚函数g、f；然后B自己实现了一个g，于是虚函数指针表的第一项本来指向A::g，现在改为指向B::g，B又包含了一个h；所以最后，B中的虚函数指针表存储的就是***B::g A::f B::h***。   
```pFun = ( Fun )*( ( int* ) * ( int* )( &b ) + i );```  
&b就是取出p的地址，然后```* ( int* )( &b )```就是强制转换为int* 类型再解析出来，就是将p转换为int类型，但p本来是指针，所以又转为int*类型，这个时候得到的就是指向了B::g的地址的int*指针，也就是虚函数指针表的第一个元素的int*指针，再进行加i是就会按照逐个指向虚函数指针表中后面的元素，```( Fun )*( ( int* ) * ( int* )( &b ) + i )```，* 将上面的int* 指针解析出来，也就得到了表中对应元素的值，( Fun )将这个值转换为Fun类型，最终结果赋给pFun；最后调用各个函数。

##5. 继承

```cpp
class Base
{
public:
 void print()
 {
  	cout<<'B'<<endl;
 }
};

class Derived: public Base
{
public:
 void print()
 {
  	cout<<'D'<<endl;
 }
}; 

int main()
{
	Derived *pd = new Derived();
	Base *pb = pd;
	pb->print();
	pd->print();
	delete pd;
	return 0;
}
```
输出：B D   
没有虚函数，前面用什么声明就调用什么的函数。

## 6. 虚函数

```cpp
class Base {
public:
	virtual void mf()
	{
		printf("B");
	}
};


class Derived : public Base {
public:
	virtual void mf()
	{
		printf("D");
	}
};
	
main()
{
	Derived *pD = new Derived;
	Base *pB = pD;
	pD->mf();
	pB->mf();
}
```
输出： D D   
虚函数的体现，pB已经指向了pD所在的内存，所以pB->mf()就会调用pD所指向对象的虚函数了。