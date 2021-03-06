---
title: C++
date: 2021-08-06 16:26:49
tags: C++
categories: 学习
description: 《黑马程序员》C++课程学习记录
cover: https://morningstarrrrr-blog-pic-1306711961.cos.ap-chengdu.myqcloud.com/a68df657aebc7e237a829501b24bb0f.jpg
---

## C++基础入门

### 常量

作用：用于记录程序中不可更改的数据

C++中定义常量两种方式：

1. #define 宏常量    ``define 常量名 常量值``

   **通常在文件上方定义**，表示一个常量

2. const 修饰的变量 ``const 数据类型 常量名 = 常量值``

   **通常在变量定义前加上关键字const**，修饰该变量为常量，不可修改



### sizeof关键字

作用：统计数据类型所占内存的大小

语法：``sizeof( 数据类型 / 变量 )``

```c++
sizeof（short）
```



### 数据类型

#### 浮点型

作用：表示小数

1. 单精度float

```C++
float f1 = 3.14f;   //在使用的时候在数字后面加上一个f
```

2. 双精度double

两者的**区别**在于表示的有效数字范围不同

| 数据类型 | 占用空间 | 有效数字范围    |
| -------- | -------- | --------------- |
| float    | 4字节    | 7位有效数字     |
| double   | 8字节    | 15~16位有效数字 |

有效数字：第一个不为零的数字开始往后数，同时最后一位要四舍五入。

**默认情况下，输出一个小数，会显示6位有效数字**



* 科学计数法

```c++
float f2 = 3e2;   //3*10^2
float f3 = 3e-2;  //3*(0.1)^2
```



#### 字符型

作用：显示单个字符

语法：``char ch = 'a'``

* 用单引号括起来，不用双引号
* 单引号内只能有一个字符，不能是字符串
* 字符型变量只占用一个字节
* 字符型变量是将字符对应的ASCII码放到存储单元中存储

‘A’的ASCII码：65         

‘a’的ASCII码：97



#### 转义字符

换行：``\n``

反斜杠：``\\``

水平制表符：``\t``   作用：在输出的时候可以让代码对齐



#### 字符串型

作用：用于表示一串字符

1. C风格字符串：``char 变量名[] = "字符串值"``

```c
char str1[] = "hello world";
```

2. C++风格字符串：``string 变量名 = "字符串值"``

```c++
#include <string>  //在C++风格字符串的时候，要包含这个文件

string str2 = "Hello World"
```



#### 布尔类型bool

作用：布尔数据类型代表真或假的值

bool类型只有两个值：

* true ：真（本质是1）
* false：假（本质是0）

**bool类型只占用1个字节大小**

```c++
bool flag = true;
bool flag = false;
```



### 运算符

#### 取模运算

#####  %：求余数

* 两个数相除除数不能为0
* 两个小数不能进行取模运算



#### 三目运算符

作用：通过三目运算符实现简单的判断

语法：``表达式1 ？ 表达式2 ： 表达式3``

解释：

如果表达式1的值为真，执行表达式2，并返回结果；

如果表达式1的值为假，执行表达式3，并返回结果。

**在C++中，三目运算符返回的是变量，可以继续赋值**





### 程序流程结构

#### switch语句

格式

```c++
switch (整型/字符型)
{
case n:
   {xxxxx;}	 //如果代码很长的话要加花括号
	break;   //重点要记得写break语句
.
.
.
case i:
	xxxxx;
	break;
default:
	xxxxx;
}

```

if 和 switch 的区别：

* switch缺点：判断的时候只能是整型或者字符型，不能是一个区间
* switch优点：结构清晰，执行效率高



#### while循环

随机数：

```c++
#include <ctime>    //头文件添加

//添加随机数种子，利用当前系统时间生成随机数，防止每次随机数都一样
srand((unsigned int)time(NULL));    

int num = rand()% 100 + 1    //在0~100之间随机生成一个数
```



#### 跳转语句

##### break语句

作用：用于跳出**选择结构**或者**循环结构**

使用的时机：

* 出现在switch语句中，作用是终止case并跳出switch
* 出现在循环语句中，作用是跳出当前的循环语句
* 出现在嵌套循环中，跳出最近的内层循环语句



##### continue语句

作用：在**循环语句**中，跳过本次循环余下尚未执行的语句，继续执行下一次循环



##### goto语句

作用：可以无条件跳转语句

语法：``goto 标记;``

解释：如果标记的名称存在，执行到goto语句时，会跳转到标记的位置

```c++
语句1；
语句2；
goto FLAG；//运行到此时跳转到下方标记处
语句3；
语句4；
FLAG；  
语句5；
```





### 数组

#### 一维数组

一维数组名称用途：

1. 可以统计整个数组在内存中的长度``sizeof(array)``
2. 可以获取数组在内存中的首地址``可以通过cout << array直接得到``



#### 冒泡排序

**作用：**最常用的算法，对数组内的元素进行排序

1. 比较相邻的元素。如果第一个比第二个大，就交换这两个元素
2. 对每一对相邻的元素做相同的工作，执行完一轮后，找到数组中最大的元素
3. 重复以上步骤，每一轮后需要比较的次数减一，直到不需要比较

**示例：**将数组{4，2，8，0，5，7，1，3，9} 进行升序排序

```c++
int main()
{
	int arr[9] = {4,2,8,0,5,7,1,3,9};
	
	for (int i = 0; i < 9 - 1; i++)  //最外层循环，一共要执行排序的轮次，元素数减1
	{
		for (int j = 0; j < 9 - 1 - i; j++)   // 内层每对元素之间依次向后比较
		{
			if(arr[j] > arr[j+1])			//比较交换
			{
				int temp = arr[j];
				arr[j] = arr[j+1];
				arr[j+1] = temp;
			}
		}
	}
}
```



#### 二维数组

二维数组定义的四种方式：

1. ``数据类型 数组名[ 行数 ][ 列数 ];``
2. ``数据类型 数组名[ 行数 ][ 列数 ] = { {数据1，数据2} ，{数据3，数据4} };``
3. ``数据类型 数组名[ 行数 ][ 列数 ] = { 数据1，数据2，数据3，数据4 };``
4. ``数据类型 数组名[  ][ 列数 ] = { 数据1， 数据2， 数据3， 数据4 };``

> 第二种更加直观，提高代码的可读性



二维数组数组名

* 查看二维数组所占程序空间
* 获取二维数组首地址

```c++
sizeof(arr)        //查看二维数组占用内存空间
sizeof(arr[0])     //查看二维数组第一行占用内存空间
sizeof(arr[0][0])  //查看第一个元素占用内存空间

sizeof(arr) / sizeof(arr[0])       //查看二维数组行数
sizeof(arr[0]) / sizeof(arr[0][0]) //查看二维数组列数

cout << (int)arr;     //查看二维数组首地址
cout << (int)arr[0];  //查看二维数组第一行首地址   不强制转换为int的话就直接输出数据了
cout << (int)arr[1];  //查看二维数组第二行首地址

cout << (int)&arr[0][0]  //查看第一个元素首地址
cout << (int)&arr[0][1]  //查看第二个元素首地址
```





### 函数

#### 概述

作用：将一段经常使用的代码封装起来，减少重复代码

一个较大的程序，一般分为若干个程序块，每个模块实现特定的功能。



#### 函数的定义

```
返回值类型 函数名（参数列表）
{
	函数体语句
	
	return表达式
}
```



#### 函数的调用

语法： 函数名称（参数）



#### 函数值传递

函数的形参发生改变，并不会影响实参



#### 函数的声明

作用：告诉编译器函数名称及如何调用函数，函数的实际主题可以单独定义

* 函数的声明可以有多次，但是函数的定义只能有一次



#### 函数的分文件编写

作用：让代码结构更加清晰

步骤：

1. 创建后缀名为.h的文件
2. 创建后缀名为.cpp的源文件
3. 在头文件中写函数的声明
4. 在源文件中写函数的定义





### 指针

#### 指针的基本概念

作用：可以通过指针间接访问内存



#### 指针变量的定义和使用

指针变量定义语法：``数据类型 * 变量名;``

解引用： *p 取指针指向地址的值



#### 指针所占内存空间

各种类型的指针所占的内存空间相同

在32位操作系统下占4个字节

在64位操作系统下占8个字节



#### 空指针

指针变量指向内存中编号为0的空间

用途：初始化指针变量

注意：空指针指向的内存是不可以访问的

```c++
int *p = NULL;
```

<font color="red">0~255号内存编号是系统占用的，不可以访问</font>



#### 野指针

指针变量指向非法的内存空间

<font color="red">在程序中要避免出现野指针</font>



#### const修饰指针

1. const修饰指针     常量指针

   * 特点：指针的指向可以修改，指针指向的值不可以修改

   ```c++
   const int *p;
   ```

2. const修饰常量     指针常量

   * 特点：指针的指向不可以修改，指针指向的值可以修改

   ```c++
   int * const p;
   ```

3. const既修饰指针，又修饰常量

   * 特点：指针的指向和指针指向的值都不可以修改

   ```c++
   const int * const p;
   ```

   



#### 指针和数组

利用指针访问数组中的元素

```c++
int arr[10] = {1,2,3,4,5,6,7,8,9,10};

int *p = arr;	//arr就是数组首地址
cout<<*p<<endl;	//输出数组中的第一个元素

p++;			//指针向后偏移4个字节
cout<<*p<<endl;	//此时输出的是数组中的第二个元素
```



#### 指针和函数

1. 值传递

2. 地址传递

   ```c++
   void swap(int *p1,int *p2){	//用指针来接收参数，因为参数是地址
   	int temp = *p1;			//用星号来解引用
   	*p1 = *p2;
   	*p2 = temp;
   }
   
   int main(){
   	int a = 10;
   	int b = 20;
   	swap(&a,&b);			//传入地址
   }
   ```

   



### 结构体

#### 结构体的基本概念

结构体属于用户自定义的数据类型，允许用户存储不同的数据类型



#### 结构体的定义和使用

语法：``struct 结构体名 {结构体成员列表};``

通过结构体创建变量的方式有三种：

* struct 结构体名 变量名 (再通过   .成员名   来进行赋值 )
* struct 结构体名 变量名 = {成员1值，成员2值……}
* 定义结构体时顺便创建变量



总结：

1. 定义结构体时的关键字是struct，不能省略
2. 创建结构体变量时，关键字struct可以省略



#### 结构体数组

作用：将自定义的结构体放入到数组中方便维护

语法：``struct 结构体名 数组名[元素个数] = { {} , {} , {} , ...{} }``

​			在{}中就将数据元素的值全部定义完成

<font color="red">结构体数组传入函数参数中的是地址</font>



#### 结构体指针

作用：通过指针访问结构体中的成员

* 利用操作符->可以通过结构体指针访问结构体属性



#### 结构体嵌套结构体

先定义被嵌套的结构体，然后再定义嵌套结构体

访问的时候直接用两个 . 号来访问嵌套结构体中的内容



#### 结构体做函数参数

1. 值传递

   ```c++
   void printstudent1(struct student s){
   	cout<<s.name<<" "<<s.age<<" "<<s.score<<endl;
   }
   
   struct student{
   	string name;
   	int age;
   	int score;
   };
   
   int main(){
   	s = ...;
       printstudent1(s);
   	
   	return 0;
   }
   ```

2. 地址传递

   ```c++
   void printstudent2(struct student *p){				//用一个指针来接收地址
   	cout<<p->name<<" "<<p->age<<" "<<p->score<<endl;	//用箭头访问
   }
   
   struct student{
   	string name;
   	int age;
   	int score;
   };
   
   int main(){
   	s = ...;
       printstudent(&s);
   	
   	return 0;
   }
   ```

   

#### 结构体中const使用场景

作用：用const来防止误操作



在用结构体做函数参数时，用地址传递，可以节省内存空间，而且不会复制一个新的副本出来

```c++
void printstudent(const student *p){	//用const可以避免对数据进行误修改
	p->name = "李四";		//此时修改不合法
	cout<<p->name;
}
```



## C++核心编程

针对C++面向对象编程技术



### 内存分区模型

C++程序在执行时，将内存大方向划分为四个区域

* 代码区：存放函数体的二进制代码，由操作系统进行管理
* 全局区：存放全局变量和静态变量以及常量
* 栈区：由编译器自动分配释放，存放函数的参数值，局部变量等
* 堆区：由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收



**内存四区意义：**

不同区域存放的数据，赋予不同的生命周期，使编程更灵活



#### 程序运行前

在程序编译后，生成了exe可执行程序，**未执行该程序前**分为两个区域

**代码区：**

​		存放CPU执行的机器指令

​		代码区是**共享**的，共享的目的是对于频繁被执行的程序，只需要在内存中有一份代码即可

​		代码区是**只读**的，使其只读的原因是防止程序意外地修改了它的指令

**全局区：**

​		全局变量和静态变量存放在此

​		全局区还包括了常量区，字符串常量和其他常量也存放在此

​		该区域的数据在程序结束后由操作系统释放



```c++
#include <iostream>
using namespace std;

//全局变量，存放在全局区中
int g_a = 10;

//const修饰的全局变量，全局常量，存放在常量区中（全局区）
const int c_g_a = 10；

int main(){
    //局部变量，不在全局区中
    int a = 10; 
    
    //静态变量，存放在全局区中
    static int s_a = 10;
    
    //常量
    //字符串常量,存放在常量区（全局区）中
    cout<<"字符串常量的地址为："<<(int)&"Hello world"<<endl;
   	
    //const修饰的变量
    //const修饰的全局变量,存放在全局区中
   
    //const修饰的局部变量,局部常量，不存放在全局区中
    const int c_l_a = 10;
    
}
```



#### 程序运行后

**栈区：**

​		由编译器自动分配释放，存放函数的参数值，局部变量等

​		注意事项：不要返回局部变量的地址，栈区开辟的数据由编译器自动释放

```c++
int* func(int b){	//形参数据也会放在栈区
    b = 100;
	int a = 10;	//局部变量
	return &a;	//返回局部变量地址
}

int main(){
	//接收func函数的返回值
    int *p = func();
    
    cout<<*p<<endl;	//第一次可以打印是因为编译器做了保留
    cout<<*p<<endl;	//第二次数据不再保留
}
```



**堆区：**

​		由程序员分配释放，若程序员不释放，程序结束时由操作系统回收

​		在C++中主要利用new在堆区开辟内存

```c++
int* func(){
    //利用new关键字，可以将数据开辟到堆区
    //指针 本质也是局部变量，放在栈上，指针保存的数据是放在堆区
   int *p =  new int(10);
   return p;
}

int main(){
    int *p = func();
    
    return 0;
}
```



#### new操作符

C++中利用new操作符在堆区开辟数据

堆区开辟的数据，由程序员手动开辟，手动释放，释放利用操作符delete

语法：``new 数据类型``

利用new创建的数据，会返回该数据类型对应的类型的指针

```c++
//1、new的基本语法
int * func(){
    //在堆区创建整型数据
    //new 返回是该数据类型的指针
    
    int *p = new int(10);
    return p;
}

void test01(){
    int *p = func();
    cout<<*p<<endl;
    //堆区的数据 由程序员开辟由程序员释放
    //如果想释放堆区的数据，利用关键字delete
    delete p;
    //cout<<*p<<endl;//内存已经被释放，不能再次访问
}

//2、在堆区用new开辟数组
void test02(){
    //在堆区创建10个整型数据的数组
    int * arr = new int[10];	//10代表元素个数
    
    //释放堆区数组，要加入中括号
    delete[] arr;
}
int main(){
    void test01;
    void test02;
    
    return 0;
}
```



### 引用

#### 引用的基本使用

**作用：**给变量起别名

**语法：**``数据类型 &别名 = 原名``

```c++
int a = 10;
int &b = a;
```



#### 引用注意事项

* 引用必须初始化

```c++
int &b; //错误
```

* 引用在初始化后不能发生改变



#### 引用做函数参数

**作用：**函数传参时，可以利用引用的技术让形参修饰实参

**优点：**可以简化指针修改实参

```c++
//值传递,形参不改变实参
void swap01(int a,int b){
	int temp = a;
	a = b;
	b = temp;
}

//地址传递
void swap02(int *a,int *b){
	int temp = *a;
	*a = *b;
	*b = temp;
}

//引用传递,形参修饰实参
void swap03(int &a,int &b){
	int temp = a;
	a = b;
	b = temp;
}

int main(){
	swap01(a,b);
	
	swap02(&a,&b);
	
	swap03(a,b);
}
```



#### 引用做函数返回值

**注意：**不要返回局部变量的引用（与 内存分区模型-程序运行后-栈区 中的例子类似，不能返回局部变量的地址）

```c++
int& test01(){
	int a = 10; //局部变量，存放在栈区
	return a;
}

int main(){
    int &ref = test01();	//test01函数的返回值也是引用类型  但是这种做法是错误的
}
```



函数调用可以作为左值存在

```c++
int& test02(){
	static int a = 10;	//静态变量，存放在全局区，程序结束后由系统释放
	return a;
}

int main(){
    int &ref = test02();
    cout<<"ref="<<ref<<endl;
    
    test02() = 1000;	//函数返回变量的引用，相当于返回变量，相当于 a = 1000；
}
```



#### 引用的本质

**本质：**引用的本质在C++内部实现是一个指针常量

```c++
void func(int &ref){
    ref = 100;	//ref是引用，转换为*ref = 100；
}

int main(){
    int a = 10;
    
    //自动转换为int * const ref = &a; 指针常量是指针的指向不能改，引用不能改的原因
    int &ref = a;
    ref = 20;	//内部发现ref是引用，转换为 *ref = 20;
}
```

C++推荐使用引用技术，因为语法方便，引用本质是指针常量，但是所有的指针操作都由编译器完成





#### 常量引用

**作用：**常量引用主要用来修饰形参，防止误操作（结构体-结构体中const使用场景类似）

在函数参数列表中，可以加const修饰形参，防止形参改变实参

```c++
void ShowValue(const int& val){
	//val = 1000;	如果形参中不加const 会对实参进行修改
    cout<<"val="<<val<<endl;
}

int main(){
	int a = 10;
	int &ref = 10;	//错误，10在常量区，不是引用合法内存空间
    int &ref = a;	//正确
    
    //加上const之后，编译器将代码修改为 int temp = 10;int &ref = temp;
    const int &ref = 10;	
    ref = 20;	//错误，加入const后变为只读，不能修改
    
    
    int a = 100;
    ShowValue(a);
}
```







### 函数提高

#### 函数默认参数

语法：``返回值类型 函数名 （形参 = 默认值）{}``

```c++
int func(int a,int b,int c = 10){
	return a + b + c;
}
```

注意事项：

1、如果某个位置已经有了默认参数，那么从这个位置往后，从左到右都必须有默认值

2、如果函数的声明有了默认参数，函数实现就不能有默认参数（声明和实现只能一个有默认参数）

```
int func2(int a = 10,int b = 10);	//函数声明

int func2(int a,int b){				//函数实现，此时就不能再用默认参数了
	return a + b;
}
```



#### 函数占位参数

函数的形参列表中可以有占位参数，但是函数调用时必须填补该位置

语法：``返回值类型 函数名 （数据类型） {}``

占位参数可以有默认参数

```c++
void func(int a,int){
	cout<<"this is func"<<endl;
}

//占位参数有默认参数
void func1(int a, int = 10){
    ......;
}
```

目前用不到，后面会用到





#### 函数重载

##### 函数重载概述

**作用：**函数名可以相同，提高复用性



**函数重载满足条件：**

* 同一个作用域下（全局、局部）
* 函数名称相同
* 函数参数 **类型不同** 或者**个数不同** 或者 **顺序不同**



**注意：**函数的返回值不可以作为函数重载的条件



##### 函数重载注意事项

* 引用作为重载条件
* 函数重载碰到默认参数

```c++
//1、引用作为重载的条件
void func(int &a){	//int &a = 10; 不合法，10在常量区
	cout<<"func(int &a)调用"<<endl;
}

void func(const int &a){	//const int &a = 10; 编译器优化，创建临时空间，合法
	cout<<"func(const int &a)调用"<<endl;
}

int main(){
    int a = 10;
    func(a);	//调用第一个函数
    
    func(10);	//调用第二个函数
}

//2、函数重载碰到默认参数
void func2(int a,int b = 10){
    cout<<"func2的调用"<<endl;
}

void func2(int a){
    cout<<"func2的调用"<<endl;
}

int main(){
    func2(10);		//错误，此时两个函数都能被调用，出现二义性，尽量避免
}					//函数重载时尽量不用默认参数
```







### 类和对象

C++面向对象的三大特性为：封装、继承、多态

C++认为万事万物都是对象，对象上有其属性和行为

**例：**

​	人可以作为对象，属性有姓名、年龄、性别…行为有走、跑、跳、吃饭

​	车也可以作为对象，属性有轮胎、方向盘…行为有载人、开空调、放音乐

​	具有<font color="red">相同性质的对象</font>，我们可以抽象为<font color="red">类</font>，人属于人类，车属于车类



#### 封装

封装是C++面向对象的三大特性之一

封装的意义：

* 将属性和行为作为一个整体，表现生活中的食物
* 对属性和行为加以权限控制



##### **封装意义1**

​	在设计类的时候，行为和属性写在一起，表现事务

**语法：**``class 类名 { 访问权限 ： 属性 / 行为 };``



例：设计一个圆类，求圆的周长

```c++
#include <iostream>
using namespace std;

const double pi = 3.14;

class Circle{
    //访问权限-公共权限
    public:
    
    //类中的属性和行为，统一称为 成员
    //属性	成员属性 成员变量
    //行为	成员函数 成员方法
    int m_r;
    
    //行为
    //获取圆的周长
    double calculateZC(){
        return 2 * pi *m_r;
    }
};		//记得分号

int main(){
    //通过圆类来创建一个具体的圆（对象）
    //实例化（通过一个类，创建一个对象的过程）
    Circle c1;
    
    //给圆对象 属性进行赋值操作
    c1.m_r = 10;
    
    //获取圆的周长
    cout<<"圆的周长为："<<c1.calculateZC()<<endl;
}
```



##### **封装意义2**

类在设计时，可以把属性和行为放在不同的权限下，加以控制

访问权限有三种：

1. public 		公共权限
2. protected   保护权限
3. private        私有权限



示例：

```c++
//公共权限 public 		成员 类内可以访问 类外可以访问
//保护权限 protected	成员 类内可以访问 类外不可以访问 儿子可以访问父亲中保护内容
//私有权限 private 		成员 类内可以访问 类外不可以访问 儿子不可以访问父亲中私有内容

class Person{
Public:   
    //公共权限
    string m_Name;	//姓名
    
Protected:
    //保护权限
    string m_car;	//汽车
    
Private:
    //私有权限
    int password;	//密码
    
Public:
    void func(){
        m_Name = "张三";
        m_Car = "比亚迪";
        m_password = "123456";
    }
};

int main(){
    //实例化一个具体的对象
    Person p1;
    p1.m_Name = "李四";		//可以访问
    //p1.m_Car = "奔驰";		//此时错误，保护权限在类外不可以访问
    //p1.m_password = "123";		//错误
}
```





struct和class的区别

在C++中struct和class的唯一区别就在于 **默认的访问权限不同**

区别：

* struct默认权限为公共
* class默认权限为私有

```c++
class C1{
  int m_A;	//默认权限为私有  
};

struct C2{
    int m_A;	//默认权限为公共
};

int main(){
    C1 c1;
    //c1.m_A = 100;	//错误,权限为私有
    C2 c2;
    c2.m_A = 100;	//正确，权限为公共
}
```





##### 成员属性设置为私有

**优点1：**将所有成员属性设置为私有，可以自己设置读写权限

**优点2：**对于写权限，我们可以检测数据的有效性



示例：

```c++
class Person{
Public:
    
    //设置姓名
    void setName(string name){
        m_Name = name;
    }
    //获取姓名
    string getName(){
        return m_Name;
    }
    
    //获取年龄 可读可写	如果想修改，年龄必须在0~150之间
    int getAge(){
        //m_Age = 0;	//初始化为0岁
        return m_Age;
    }
    
    //设置年龄
    void setAge(int age){
        if(age < 0 || age > 150){
            m_Age = 0;
            cout<<"年龄有误"<<endl;
            return ;
        }
        m_Age = age;
    }
    
    //设置情人 只写
    void setLover(string lover){
        m_Lover = lover;
    }
    
Private:
    //姓名	可读可写
    String m_Name;
    //年龄	只读
    int m_Age;
    //伴侣	只写
    string m_Lover;
};

int main(){
    Person p;
    //p.m_Name = "张三";	//错误 私有权限不能访问
    p.setName("张三");	//正确 公共权限函数访问
    cout<<"姓名为："<<p.getName()<<endl;
    
    //p.m_Age = 18;		//错误 私有权限不能访问
    //p.setAge(18);		//错误 没有这个函数		
    cout<<"年龄为："<<p.getAge()<<endl; 
    
    //设置情人
    p.setLover("李四");
    //cout<<"情人为："<<p.m_Lover<<endl;	//错误 私有权限不能访问
}
```



##### 头文件与源文件分离

头文件.h中写函数定义

```c++
#pragma once		//为了避免一个头文件被包含多次
#include <iostream>
using namespace std;
#include <xxx.h>	//若其中使用到了其他类的内容，只需要包含所用类的头文件

void func();		//只做函数声明
```



cpp文件中写函数实现

```c++
#include <xxx.h>

void xxx::func(){	//xxx:: 说明是成员函数
	//函数实现
}
```







#### 对象特性

C++中的面对对象来源于生活，每个对象有初始设置和对象销毁前的清理数据的设置



##### 构造函数和析构函数

对象的**初始化和清理**也是两个非常重要的安全问题

​	一个对象或者变量没有初始状态，对其使用后果是未知

​	同样的使用完一个对象或变量，没有即时清理，也会造成一定的安全问题



C++利用构造函数和析构函数解决上述问题，这两个函数将会被编译器自动调用，完成对象初始化和清理工作。对象的初始化和清理工作是编译器强制要我们做的事情，因此如果**我们不提供构造和析构，编译器提供的构造和析构函数是空实现**



* 构造函数：主要作用在于创建对象时为对象的成员属性赋值，由编译器自动调用，无须手动
* 析构函数：主要作用在于对象**销毁前**自动调用，执行一些清理工作



构造函数语法：``类名(){}``

1. 构造函数，没有返回值也不写void
2. 函数名称和类名相同
3. 构造函数可以有参数，因此可以发生重载
4. 程序在调用对象的时候会自动调用构造，无须手动调用，而且只会调用一次
5. 前面要写作用域



析构函数语法：``~类名(){}``

1. 析构函数，没有返回值也不写void
2. 函数名称和类名相同，在名称前面多加一个~
3. 析构函数不能有参数，不能发生重载
4. 程序在对象销毁前会自动调用析构，因此无须手动调用，而且只会调用一次





##### 构造函数的分类及调用

两种分类方式：

​	按参数分为：有参构造和无参构造

​	按类型分为：普通构造和拷贝构造

三种调用方式：

​	括号法

​	显示法

​	隐式转换法



分类

```c++
class Person{
public:	
    Person(){
        cout<<"无参函数构造调用"<<endl;
    }
    Person(int a){
        age = a;
        cout<<"有参函数构造调用"<<endl;
    }
    //拷贝构造函数
    Person(const Person &p){	//避免对p本身进行修改，结构体中const的应用 类似
        //将传入的人身上的所有属性，拷贝到自身
        age = p.age;
        cout<<"拷贝构造函数调用"<<endl;
    }
    
    ~Person(){
        cout<<"析构函数调用"<<endl;
    }
};
```





调用

```c++
void test01(){
	//1、括号法
    Person p1;	//函数默认构造函数调用
    Person p2(10);	//有参构造函数
    //拷贝构造函数调用
    Person p3(p1);
    
    //注意事项1
    //调用默认构造函数时，不要加括号（）
    //Person p1();	//这行代码会被认为是函数的声明，不会认为是在创建对象
    
    //2、显示法
    Person p1;
    Person p2 = Person(10);	//有参构造
    Person p3 = Person(p2);	//拷贝构造
    
    Person(10);	//匿名对象 特点，当前行执行结束后，系统会立即回收掉匿名对象
    //注意事项2
    //不要利用拷贝构造函数 初始化匿名对象 编译器会认为Person(p3) === Person(p3);
    //编译器会认为是对象的声明
    Person(p3);
    
    //3、隐式转换法
    Person p4 = 10;	//相当于写了 Person p4 = Person(10);
    Person p5 = p4;
}
```



##### 拷贝构造函数调用时机

C++中拷贝函数调用时机通常有三种情况

* 使用一个已经创建完毕的对象来初始化一个对象
* 值传递的方式给函数参数传值
* 以值方式返回局部对象

```c++
class Person{
public:
    Person(){
        cout<<"Person的默认构造函数调用"<<endl;;
    }
    
    Peson(int age){
        cout<<"Person的有参构造函数调用"<<endl;
        m_Age = age;
    }
    
    Person(const Person &p){
        cout<<"Person的拷贝构造函数调用"<<endl;
        m_Age = p.m_Age;
    }
    
    ~Person(){
        cout<<"Person的析构函数调用"<<endl;
    }
    
    int m_Age;
}

//1.使用一个已经创建完毕的对象来初始化一个新对象
void test01(){
    Person p1(20);
    Person p2(p1);
}

//2.值传递的方式给函数参数传值
void doWork(Person p){
    
}

void test02(){
    Person p;
    doWork(p);
}

//3.值方式返回局部对象
Person doWork2(){
    Person p1;
    cout<<(int*)&p1<<endl;
    return p1;
}

void test03(){
	Person p = doWork2();
    cout<<(int*)p <<endl;
}
```





##### 构造函数的调用规则

默认情况下，c++编译器至少给类添加三个函数

1.默认构造函数（无参，函数体为空）

2.默认析构函数（无参，函数体为空）

3.默认拷贝构造函数，对属性进行值拷贝



构造函数调用规则：

* 如果用户定义有参构造函数，c++不再提供默认无参构造，但是会提供默认拷贝构造
* 如果用户定义拷贝构造函数，c++不再提供其他构造函数



```c++
//构造函数的调用规则
//1.创建一个类，c++编译器会给每个类都添加至少三个函数
//默认构造 （空实现）
//析构函数 （空实现）
//拷贝构造 （值拷贝）
    
//2.如果我们写了有参构造函数，编译器就不再提供默认构造，依然提供拷贝构造


class Person{
public:
	Person()
	{
		cout << "Person的默认构造函数调用" << endl;
	}

	Person(int age)
	{
		cout << "Person的有参构造函数调用" << endl;
		m_Age = age;
	}

	Person(const Person &p)
	{
		cout << "Person的拷贝构造函数调用" << endl;
		m_Age = p.m_Age;
	}

	~Person()
	{
		cout << "Person的默认析构函数调用" << endl;
	}

	int m_Age;

};

void test01()
{
	Person p;
	p.m_Age = 18;

	Person p2(p);

	cout << "p2的年龄是：" << p2.m_Age << endl;
}


void test02()
{
    Person p;	//如果有 有参构造函数定义，没有自己定义的默认构造函数，就会报错，因为
    			//此时系统也不会提供默认构造函数
    
}
```





##### 深拷贝和浅拷贝

浅拷贝：简单的赋值拷贝操作

深拷贝：在堆区重新申请空间，进行拷贝操作



```c++
class Person{
public:
	Person()
	{
		cout << "Person的默认构造函数调用" << endl;
	}

	Person(int age, int height)
	{
		cout << "Person的有参构造函数调用" << endl;
		m_Age = age;
        m_Height = new int(height);
	}
    
    //自己实现拷贝构造函数 解决浅拷贝带来的问题
    Person(const Person &p)
    {
        cout<< "Person 拷贝构造函数调用"<<endl;
        m_Age = p.m_Age;
        //m_Height = p.m_Height;	编译器默认实现就是这行代码
        
        //深拷贝操作
        m_Height = new int(*p.m_Height);	//解引用来获得m_Height的值
    }

	//Person(const Person &p)
	//{
	//	  cout << "Person的拷贝构造函数调用" << endl;
	//	  m_Age = p.m_Age;
	//}

	~Person()
	{
        //析构代码，将堆区开辟的数据做释放操作
        if(m_Height != NULL)
        {
            delete m_Height;
            m_Height = NULL;	//防止野指针出现
        }
		cout << "Person的默认析构函数调用" << endl;
	}

	int m_Age;
    int *m_Height; //new新建开辟到堆区，用指针接收

};

void test01()
{
    Person p1(18,160);
    cout<<"p1的年龄为:"<<p1.m_Age<<"  身高为:"<<p1.m_Height<<endl;
    
    Person p2(p1);
    cout<<"p2的年龄为:"<<p2.m_Age<<"  身高为:"<<p2.m_Height<<endl;
    //此时会出错 默认拷贝函数将 int *m_Height 中的全部内容拷贝过去
    //p2 和 p1 在函数运行结束后都会进行析构函数释放 m_Height 内存的操作 
    //重复释放，非法操作
}
```



浅拷贝带来的问题就是堆区的内存重复释放

<font color="red"> 浅拷贝的问题，要利用深拷贝来进行解决</font>，即给使用拷贝构造的函数也申请一块新的内存空间



**总结：**

<font color="red">如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题</font>





##### 初始化列表

作用：用来初始化属性



**语法：**`` 构造函数():属性1(值1)，属性2(值2)...{}``

```c++
class Person
{
public:
    //传统初始化操作
    Person(int a, int b, int c)
    {
        m_A = a;
        m_B = b;
        m_C = c;
    }
    
    int m_A;
    int m_B;
    int m_C;
    
    //初始化列表初始化属性
    Person():m_A(10),m_B(20).m_C(30)
    {
        
    }
    
    //更灵活的方式初始化列表初始化属性
    Person(int a, int b, int c):m_A(a),m_B(b).m_C(c)
    {
        
    }
};

	

void test01(){
    //Person p(10,20,30);	普通构造
    Person p;				初始化列表构造
    Person p(30,20,10);		第三种构造
    cout<<"m_A = "<<p.m_A<<endl;
    cout<<"m_B = "<<p.m_B<<endl;
    cout<<"m_C = "<<p.m_C<<endl;
}
```





##### 类对象作为类成员

C++中的成员可以是另一个类的对象，我们称该成员为 对象成员



例如：

```c++
class A{}
class B{
	A a;
}
```



B类中有对象A作为成员，A为对象成员



```c++
class phone{
public:
	phone(string PName){
		m_PName = pName;
	}
	
	string m_PName
};

class Person{
public:
    
    //Phone m_Phone = pName;	隐式转换法
    Person(string name, string pName):m_Name(name),m_Phone(PName)
    {
        
    }
    
	//姓名
	string m_Nname;
	//手机
	Phone m_Phone;
};

void test01(){
    Person p("张三","苹果")；
}
```



<font color="red">其他类的对象作为本类的成员时，构造时候先构造类对象，再构造自身，析构的顺序与构造相反，先析构本类，然后在析构其他类</font>





##### 静态成员和静态成员函数

静态成员就是在成员变量和成员函数前加上关键字static，称为静态成员

静态成员分为：



* 静态成员变量
  * 所有对象共享同一份数据
  * 在编译阶段分配内存
  * 类内声明，类外初始化
* 静态成员函数
  * 所有对象共享同一个函数
  * 静态成员函数只能访问静态成员变量



```c++
class Person{
public:
	
	//静态成员函数
	static void func()
	{
        m_A = 100; //静态成员函数可以访问静态成员变量
        //m_B = 200; //静态成员函数 不可以访问 非静态成员变量，无法区分到底是哪个对象的m_B属性
		cout<<"static void func调用"<<endl;
	}
    
    static int m_A;	//静态成员变量
    int m_B; //非静态成员变量
    
    //静态成员函数也是有访问权限的
private:
    static void func2(){
        cout<<"static void func2()调用"<<endl;
    }
};

int Person::m_A = 0; //类外初始化

//两种访问方式
void test01()
{
	//1.通过对象访问
    Person p;
    p.func();
    //2.通过类名访问
    Person::func();
    
    //Person::func2();	//类外访问不到私有静态成员函数
}

int main(){
    test01;
    
    return 0;
}
```







#### C++对象模型和this指针

##### 成员变量和成员函数分开存储

在C++中，类内的成员变量和成员函数分开存储

只有非静态成员变量才属于类的对象上

```c++
class Person{

    
    int m_A;	//非静态成员变量 属于类的对象上 只要不是空，就是原大小
    
    static int m_B;	//静态成员变量 不属于类的对象上
    88
    void func(){}	//非静态成员函数 不属于类的对象上
    
    static void fun2(){}	//静态成员函数 不属于类的对象上
};

void test01(){
	Person p;
	//空对象占用空间内存空间为：1
    //C++编译器会给每个空对象分配一个字节空间，是为了区分空对象占内存的位置
    //每个空对象也应该有一个独一无二的内存地址
	cout<<"size of p = "<<sizeof(p)<<endl;
}

void test02(){
    Person p;
	cout<<"size of p = "<<sizeof(p)<<endl;
}

int main(){
	//test01();
    test02();
}
```





##### this指针概念

 每一个非静态成员函数只会诞生一份函数实例，即多个同类型的对象会共用同一块代码，那么这一块代码如何区分哪个对象调用自己呢？



C++通过提供特殊的对象指针，this指针来解决该问题。**this指针指向被调用的成员函数所属的对象**



this指针是隐含在每一个非静态成员函数内的一种指针

this指针不需要定义，直接使用即可



this指针的用途：

* 当形参和成员变量同名时，可以用this指针来区分
* 在类的非静态成员函数中返回对象本身，可以使用return *this



```c++
class Person
{
Public:
	Person(int age)
	{
		age = age;
	}
	
	int age;	//与构造函数中的参数相同了，应该加以区分 可以使用m_Age
				//m代表member
	
	//这里要加&符号 不加&代表以值的方式返回，会复制一份新的数据返回
    //相当于返回的不是p2 而是p2'	引用的方式不会创建新的对象
    Person& PersonAddAge(Person &p){
        this->age += p.age;
        
        //this是指向p2的指针，而*this指向的就是p2这个对象本体
        return *this;
    }

};				

正确的写法：
Public:
	Person(int age){
        //this指针指向被调用的成员函数所属的对象	这里this指向p1
        this->age = age;
    }

//1.解决名称冲突
void test01(){
	Person p1(18);
    cout<<"p1的年龄为："<<p1.age<<endl;
}

//2.返回对象本身用 *this	可以一直做追加操作
void test02(){
    Person p1(10);
    
    Person p2(10);
    
    //链式编程思想
    p2.PersonAddAge(p1).PersonAddAge(p1).PersonAddAge(p1);
    
    cout<<"p2的年龄为："<<p2.age<<endl;
}

int main(){
    test01();
    
    test02();
}

```

