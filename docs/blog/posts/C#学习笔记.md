---
date: 
    created: 2024-07-31
authors: [wanghx]
draft: false
counter: false
comments: false
---
# C# 学习笔记

大一短学期课程（Windows C# 程序设计）学习笔记。
<!-- more -->

## 第二章 语法基础与数据类型

### 2.1 语法基础

- C#文件后缀：.cs
- 编译命令：csc
- 导入命名空间（以System为例）：`using System;`
- 类和命名空间可嵌套，例如：`System.Data`是嵌套在 `System`下的一个命名空间
- C#要求每个程序必须且只能有一个“Main”方法。“Main” 方法必须放在某一个类中，是应用程序的入口

  `static void Main(string［］args)`

### 2.2 数据类型

C#的每种数据类型都可以看做一个类，每个类都有对应的方法可供调用。

所有变量需声明后再使用。

#### 2.2.1 整数类型

| 类型名 | 类型名                |
| ------ | --------------------- |
| sbyte  | 有符号字节型（1字节） |
| byte   | 无符号字节型（1字节） |
| short  | 短整型                |
| ushort | 无符号短整型          |
| int    | 整型                  |
| uint   | 无符号整型            |
| long   | 长整型                |
| ulong  | 无符号长整型          |

#### 2.2.2 实数类型

| 类型名  | 类型名       |
| ------- | ------------ |
| float   | 单精度浮点型 |
| double  | 双精度浮点型 |
| decimal | 十进制型     |

#### 2.2.3 其它类型

| 类型名 | 类型名                   |
| ------ | ------------------------ |
| char   | 一个Unicode字符（2字节） |
| bool   | 布尔类型（true/false）   |
| string | 字符串                   |

#### 2.2.4 结构型:struct

```C#
//结构型的定义
struct Student
{
    public int no;
    public string name;
}

//结构型变量的定义
Student s;
//结构的使用
s.no=3230106032;
s.name="WangHX";
```

### 2.3 数组

#### 2.3.1 一维数组

- 一维数组的声明和初始化

```C#
//一维数组的声明
int [] array1=new int[10];

//初始化法一：声明时初始化
int []array1={1,2,3,4,5,6,7,8,9,10};

//初始化法二：先声明后初始化
int []array1;
array1=new int[10]{1,2,3,4,5,6,7,8,9,10};

//初始化法三：先创建后初始化
int [] array1=new int[10];
for(int i=0;i<10;i++)
    array[i]=i+1;
```

- Array类提供的方法

  | 方法        | 用途                       |
  | ----------- | -------------------------- |
  | Length      | 获得数组长度               |
  | Clear       | 清除数组元素的值           |
  | Copy        | 复制数组                   |
  | Sort        | 排序（仅一维数组）         |
  | Reverse     | 翻转数组元素（仅一维数组） |
  | IndexOf     | 从左查找字符（仅一维数组） |
  | LastIndexOf | 从右查找字符（仅一维数组） |
  | Resize      | 更改数组长度（仅一维数组） |

#### 2.3.2 多维数组

```C#
//二维数组的声明（更高维类似）
int [,] array2=new int [3,4];

//初始化法一：声明时初始化
int [,] array2={{1,2,3,4}，{5,6,7,8}，{9,10,11,12}};

//初始化法二：先声明后初始化
int [,] array2;
array2=new int [3,4]{{1,2,3,4}，{5,6,7,8}，{9,10,11,12}};

//元素的访问
int x=array2[1,2];	//x=7
```

#### 2.3.3 数组的数组

```C#
//二维数组型数组的声明（更高维类似）
int [][] array3=new int [3][4];

//初始化例子
int [][] array4={
    new int[]{1,2,3},
    new int[]{4,5,7,8},
    new int[]{6}
};

//元素的访问
int x=array4[1][2];	//x=7
```

#### 2.3.4 数组元素的遍历：foreach语句

```C#
int [] list={1,2,3,4,5};
foreach(int i in list)
    Console.WriteLine(i);

//该程序逐个输出1,2,3,4,5
```

### 2.4 字符串

- 字符串是由Unicode字符组成的字符数组，使用string声明、双引号标记，允许通过索引来提取字符串中的字符。
- 字符串是不可变的，一旦创建就不可更改。
- 两个字符串可用“+”连接，用关系运算符“==”、!=”进行比较

  ```C#
  //例：在Console.Write方法中使用字符串连接
  Console.Write(Name + ",您好！");
  ```

- System.String提供的方法

  | 方法        | 用途             |
  | ----------- | ---------------- |
  | Length      | 获得字符串长度   |
  | Copy        | 复制字符串       |
  | IndexOf     | 从左查找字符     |
  | LastIndexOf | 从右查找字符     |
  | Insert      | 插入字符         |
  | Remove      | 删除字符         |
  | Replace     | 替换字符         |
  | Split       | 分割字符串       |
  | Substring   | 取子字符串       |
  | Trim        | 压缩字符串的空白 |
  | Format      | 格式化字符串     |

### 2.5 类型转换

- 隐式转换：允许数值范围小的类型向数值范围大的类型转换、无符号整数类型向有符号整数类型转换。
- 显式转换：可能导致数据丢失，例如：`int x=600;	short z=(short)x;`
- 使用方法转换

  - Parse方法：将符合格式要求的字符串转换为数值。例如：`int x=int.Parse("123.4");`
  - ToString方法：将其它类型变量值转换为字符串类型。例如：`int x=123;	string s=x.ToString();`
  - Convert方法

    ```C#
    int val;
    val=Convert.ToInt32(Console.ReadLine());
    ```

### 2.6 运算符

- &&、&、||、|、^，都是逻辑运算符，分别表示逻辑与、逻辑或、逻辑异或。
- ||、|的主要区别：当第一个操作数为true时，前者不再计算第二个操作数的值。
- &&和&的主要区别：当第一个操作数为false时，前者不再计算第二个操作数的值。

## 第三章 命名空间

### 3.1 命名空间的声明

```C#
//命名空间的声明可以嵌套，下述等价：

//法一：
namespace SpaceName
{
    namespace Inner
    {...}
}

//法二：
namespace SpaceName{...}
namespace SpaceName.Inner{...}
```

- 在命名空间内引用其它已定义好的命名空间，引用命令（using）必须放在最前面
- 若多个命名空间的完整名称相同，则这几个命名空间为同一个命名空间
- 命名空间的成员：类、结构、接口等


### 3.2 命名空间的使用

- using指令的有效范围：该指令所属的编译单元或命名空间
- 使用using指令设置别名

  ```C#
  using 别名=命名空间名或类型名;
  ```

- 使用using指令引入命名空间

  ```C#
  using 命令空间名;
  ```

- using指令只能导入命名空间本身，不会导入嵌套的命名空间

### 3.3 动态链接库

在Visual Studio创建项目时，选择创建动态链接库，可以以命名空间为单位，将其内容（如类）封装到动态链接库（dll）中

其它程序引用动态链接库后，可以使用动态链接库中的类等内容

## 第四章 类

### 4.1 类的声明和可访问性

- 格式：`[属性][类修饰符] class 类名 {内容...}`

  ```C#
  public class Student
  {
     public int SNO;	//定义实例成员
     public static int count; 	//定义静态成员
     public Student(int s)	//定义构造函数
     {   SNO=s;
         count++;
     }
     public void display()	//定义方法
     {
        Console.WriteLine("count={0},SNO={1}", count, SNO);
     }
     ~Student()	//定义析构函数
     {
         count--;
     }
  }
  ```

- 类和类成员的访问修饰符

  - public：公有，访问不受限制
  - private：（成员的默认）私有，只能从同一类中访问
  - protected：保护，只能从同一类和派生类中访问
  - internal：（类的默认）内部，只能从同一项目中访问

- 类的特殊修饰符

  - abstract：不能实例化，只能继承
  - sealed：不能继承（称为密封类）

    对类中的方法使用sealed修饰，则该方法不能在派生类中被重写

### 4.2 类的成员

类成员包括**数据成员**和**函数成员**，具体如下：

- 数据成员：常量、变量
- 函数成员：方法、属性、索引器、运算符、构造函数、析构函数

#### 4.2.1 构造函数

- 在创建对象时首先执行（自动），完成对象的初始化操作
- 其名称为 `类名`
- 构造函数可以重载，但不能继承
- 构造函数可以带参数，但没有返回值，不用声明返回类型
- 构造函数的类型修饰符总是public，如果是private则表示这个类不能被实例化

#### 4.2.2 析构函数

- 在对象被销毁之前最后执行（自动），完成对象结束的收尾工作
- 其名称为 `~类名`
- 析构函数不能重载、继承
- 析构函数不带参数，没有返回值
- 析构函数不用加类型修饰符

#### 4.2.3 方法

- 必须声明方法的返回值类型，包括void；若返回值非void，必须有return语句
- 方法的调用

  - 调用者是同一个类的方法：直接调用
  - 调用者是其它类的方法：通过类的实例来引用，静态方法通过类名直接调用
- 方法的参数传递

  ```C#
  //值参数传递:调用前a=1，调用后a=1
  void func(int a)
  {	a++;	}
  
  //引用参数传递:调用前a=1，调用后a=2
  void func(int a)
  {	a++;	}
  
  //输出参数传递:调用前a=1、b=2，调用后sum=3
  void add(int a，int b,out int sum)
  {	sum=a+b;	}
  
  //参数数组传递：适用于参数个数未知的情形
  void func(params int[] array)
  ```

- 方法的重载

  重载的方法名称必须相同，形参的个数或类型必须不同

#### 4.2.4 属性

```C#
class MyClass
{     private int Num = 0;
       public int StuNum	//int:属性的数据类型
       {
            get		//get用于获取属性，用return返回值
            {
                   return Num;	//num的类型与属性的数据类型一致
            }
            set		//set用于设置属性，用value赋值
            {  
            	if (value > 0)	number = value;
            }
      }
}

//get访问器和set访问器不必须同时存在

//使用示例：
MyClass me=new Myclass();
me.StuNum=5;	//调用set访问器
Console.WriteLine(me.StuNum);	//调用get访问器
```

### 4.3 类的静态成员和实例成员

- 静态成员
  - 用static修饰符声明的成员为静态成员
  - 静态成员属于类，为这个类的所有实例所共享
  - 静态成员只能由类来调用，不能由对象调用，调用方法为 `类名.静态成员名`
  - 静态方法：不创建对象的情况下就可以调用该方法，不能访问实例成员，只能访问静态成员
  - 静态构造函数：用于初始化静态成员，一个类只能有一个静态构造方法，没有修饰符和参数，会在程序创建第一个实例或引用任何静态成员之前，完成类中静态成员的初始化
  - Main方法是静态方法，这使得无需创建对象就可以运行程序
- 实例成员
  - 不用static修饰符声明的成员为实例成员
  - 实例成员属于类的实例的成员

### 4.4 静态类

- 静态类使用static关键字来声明，它仅包含静态成员，不能实例化
- 静态类不能包含构造函数，可以包含静态构造函数

### 4.5 类的实例化

#### 4.5.1 对象的声明与创建

```C#
//声明一个Student对象stu1，并为其分配内存空间
Student stu1=new Student(参数表);	//参数表中的参数传递给构造函数
```

#### 4.5.2 类成员的内部访问：this关键词

一个类成员要使用当前类的其它成员，可以采用this关键词，this指代的是当前对象

```C#
		static void Main(string[] args)
        {
            Console.Write("请输入你的名字：");
            string name=Console.ReadLine();
            Person p = new Person(name);//利用构造函数传递参数
            p.Print();
        }
        class Person
        {
            private string name;
            public Person(string name)//一个参数的构造函数
            {
                this.name = name;
                //形参名字与类中字段名字相同，为了区分类中的属性和形参使用this
            }
            public void Print()
            {
                Console.WriteLine("我的名字叫：" + this.name);
            }
        }
```

### 4.6 派生类

#### 4.6.1 派生类的声明

- 格式：`[属性][类修饰符] class 类名:基类名 {内容...}`

  ```C#
  class NewClass:OldClass
  {
      //派生类新增的成员
  }
  ```

- 类继承的原则

  - 只能指定一个基类
  - 可以继承基类的所有方法、字段、属性、事件等
  - 派生类可以拓展基类的成员，也可以重写基类的方法成员
  - 不继承基类的构造函数
  - 可以继承多代

#### 4.6.2 派生类的构造函数

- 在派生类中对新增成员进行初始化，由派生类的构造函数完成;在派生类中对基类成员进行初始化，由基类的构造函数完成
- 创建派生类对象时，首先执行基类的构造函数，随后再执行派生类的构造函数

```C#
 派生类名(参数总表)[:base(参数表)]
  {
     // 派生类新增成员的初始化语句
  }
```

- 默认情况下，派生类的所有构造函数会自动调用基类的无参构造函数。当派生类的有参构造函数需要调用基类的有参构造函数时，需要在定义派生类构造函数时，缀上基类名base及其有参构造函数的初始化列表。如：

  `public Car(int w, int p, string id):base(w,p,id)`

### 4.7 分部类

- 分部类允许将类的定义拆分到多个源文件中，让每个源文件只包含类型定义的一部分，编译时编译器自动把所有部分组合起来进行编译。
- 同一类型的各个部分的所有分部类的定义都必须使用 `partial`进行修饰

## 第五章 多态性及实现

### 5.1 概述

- 多态性：类中具有相似功能的不同函数使用同一名称来实现，从而可以使用相同的调用方式来调用这些具有不同功能的同名函数
- 多态性的实现方式有以下几种：
  - 通过继承实现多态性（虚方法、隐藏基类的方法）
  - 通过抽象类实现多态性

### 5.2 虚方法

- 使用 `new`关键字定义与基类中同名的成员，则可替代基类的成员
- 在基类中，如果想让某个方法被派生类重写，可以使用关键字 `virtual`声明该方法为虚方法，并在派生类中用 `override`关键词重写

```C#
//基类中的方法（虚方法）
public virtual 返回值类型 方法名()
{	...	}

//派生类中重写的方法
public override 返回值类型 方法名()
{	...	}
```

- 派生类中，虚方法不必须被重写
- 重写方法的名称、参数个数、类型、返回值必须和虚方法一致

```C#
//例：车辆管理系统
class Vehicle //定义车基类
{       protected int passengers;  //乘客数
        protected string videntifier;//标志
        public Vehicle(int p, string id)
        {   
            videntifier = id;
            passengers = p;
        }
        public virtual void Speak() {   }
        public void Print()
        {   
            Console.WriteLine("乘客数：" +passengers);  
            Console.WriteLine("标志：" +videntifier); 
        }
}

class Truck:Vehicle  //定义卡车类
{
        private float load;         //私有成员：载重量
        public Truck(int p, float l, string id): base(p, id)
        {          
            load = l;
        }
        public override void Speak()
        {
            Console.WriteLine("卡车鸣笛：叭叭叭叭!");
        }
        public new void Print()
        {
            base.Print();	//调用基类的方法
            Console.WriteLine("载重：" +load);
        }
}
```

### 5.3 隐藏基类的方法

- 在派生类中，可以使用 `new`关键字来隐藏（取代）基类的同名方法
- 使用 `new`关键字时并不要求基类中的方法声明为 `virtual`，只要在派生类的方法前声明为 `new`，就可以隐藏基类的方法

```C#
//例：
class Hello
{     public void SayHello()
       {    Console.WriteLine("这是基类!");       }
}
class New Hello : Hello
{     public new void SayHello()
       {    Console.WriteLine(“这是派生类!");    }
}  
```

### 5.4 抽象类

#### 5.4.1 抽象类的含义和声明

- 抽象方法：在基类的定义中，不包含任何实现代码的方法。其唯一的作用是统一接口（参数）形式，让派生类重写
- 抽象属性：在基类的定义中，不提供属性访问器的实现。它只声明该类支持的属性，而将访问器的实现留给派生类
- 抽象类：含有至少一个抽象成员（抽象方法、抽象属性）的类，它要求派生类提供某些或者全部抽象成员的实现。在抽象类中，也可声明非抽象成员

  ```C#
  //抽象属性的声明
  public abstract 返回值类型 属性名
  {
  	get;
  	set；
  }
  
  //抽象类和抽象方法的声明
  public abstract class 抽象类名
  {
  	[访问修饰符] abstract 返回值类型 方法名（[参数列表]）
  }
  
  //抽象方法在派生类中的实现
  public override 返回值类型 方法名（[参数列表]）
  {	...	}
  ```

#### 5.4.2 重载抽象方法

- 当定义抽象类的派生类时，派生类必须重载基类所有的抽象方法和抽象属性（如果派生类没有进行重载，则派生类也必须声明为抽象类）
- 抽象类不能实例化，当其派生类给出了所有的抽象成员的实现后，这个派生类才可实例化

## 第六章 Windows应用程序设计基础

### 6.1 窗体

C#中以类Form来封装窗体，用户设计的窗体都是类Form的派生类，用户窗体中添加其他界面元素的操作实际上就是向派生类中添加私有成员

#### 6.1.1 窗体的属性

- Name：名称（代码调用时的名称）
- Text：标题（在标题栏显示）
- ControlBox、MaximizeBox、MinimizeBox：设置窗体上是否有控制菜单、最大最小化按钮
- FormBorderStyle：控制窗体边界类型
- Visible：设置窗体的可见性

#### 6.1.2 窗体的事件

- Click：窗体单击
- DoubleClick ：窗体双击
- KeyPress：键盘击键
- KeyDown、MouseDown：键盘、鼠标键按下
- FormClosing、FormClosed：窗体正在、已经关闭

  （窗体关闭方法被调用前，触发FormClosing事件，此时可进行资源的释放和清理，也可弹出提示框询问是否关闭窗体）

  ```C#
  private void Form1_FormClosing(object sender, FormClosingEventArgs e)
  {
       DialogResult dr = MessageBox.Show("是否关闭窗体", "提示",
            MessageBoxButtons.YesNo, MessageBoxIcon.Warning);
       if (dr == DialogResult.Yes) //使用if语句判定是否单击“是”按钮
       {
              e.Cancel = false;　  //如果单击“是”按钮则关闭窗体
       }
        else　　
        {
              e.Cancel = true;　　//否则，不执行操作
        }
  }
  ```
- Load ：窗体加载（窗体第一次显示前，触发该事件，此时可对窗体进行界面和数据的初始化）
- LocationChanged ：窗体位置改变
- Resize：窗体大小改变

#### 6.1.3 多个窗体

- 设置启动窗体

  ```C#
  //FileName:Program.cs
  static class Program
  {
       static void Main()
       {
           Application.EnableVisualStyles();
           Application.SetCompatibleTextRenderingDefault(false);
           Application.Run(new Form1());	//Form1即为指定的启动窗体（任何窗体在启动前必须实例化）
       }
   }
  ```

- 模式窗体与非模式窗体

  - 模式窗体：处于活动状态时，程序不能切换到其他窗体中（例如一些对话框）
  - 非模式窗体：处于活动状态时，程序能切换到其他窗体中
- 在一个窗体中打开另一个窗体

  ```C#
  Form2 fm=new Form2();	//实例化Form2
  fm.Show();			//调用Show方法显示Form2窗体，此时打开的是非模式窗体
  fm.ShowDialog();	//调用Show方法显示Form2窗体，此时打开的是模式窗体
  ```

- 窗体的隐藏：hide()方法

  ```C#
  this.Hide();	//隐藏当前窗体
  fm.Hide();	//隐藏其它窗体（以fm为例）
  ```

- 窗体的关闭：close()方法

### 6.2 窗体控件的通用属性

- 所有窗体控件全部继承于System.Windows.Forms.Control类
- Anchor（锚）属性：确定当前控件与其容器控件的上、下、左、右四边距离的固定关系
- Dock属性：确定当前控件与其容器控件的边缘融合关系

### 6.3 常用控件

#### 6.3.1 Button：按钮

- Button的属性：

  - Text：设定按钮上显示的文本。该属性也可为按钮创建快捷方式。

    - 某个按钮的Text属性设置为“&Display”，程序运行时，就会显示为“`<u>`D`</u>`isplay”，按Alt+D即可激活按钮
    - 某个按钮的Text属性设置为“文件（&F)"，程序运行时，就会显示为”文件（F）“，按Alt+F即可激活按钮
  - FlatStyle：设定按钮的外观风格

#### 6.3.2 Label：标签

- Label的属性：

  - Text：显示的文本
  - BorderStyle：设定标签的边框样式
  - BackColor、ForeColor：设定标签背景、文本的颜色
  - Font：设定标签文本字体

#### 6.3.3 TextBox：文本框

- 文本框的属性：

  - Text：设定文本框显示的文本
  - BackColor、ForeColor：设定文本框背景、文本的颜色
  - Font：设定文本框文本字体
  - PasswordChar：密码输入模式
  - ReadOnly：设定文本框控件是否只读
  - MultiLine：设定文本框是否包含多行文本
- 文本框的方法：

  - Clear：清空文本
  - AppendText：用于文本框最后追加文本
- 文本框的事件：

  - TextChanged：文本框的文本内容发生变化
  - Enter、Leave：文本框获得、失去焦点

#### 6.3.4 RadioButton：单选按钮

- 单选按钮控件总是成组出现。直接添加到一个窗体中的所有单选按钮将形成一个组。若要添加不同的组，必须将它们放到面板或分组框（GroupBox控件）内
- 单选按钮的属性：
  - Text：设定按钮的说明文字
  - Check：布尔类型，表示按钮是否被选中
- 单选按钮的事件：
  - Click：鼠标点击单选按钮
  - CheckedChanged：Checked属性值发生改变

#### 6.3.5 CheckBox：复选按钮

属性和事件同单选按钮

#### 6.3.6 ListBox：列表框

- 列表框是一个项目列表，每一项按照加入列表的先后顺序有一个索引号（从0开始）
- 属性：
  - Items：列表项，可在属性面板进行添加与设置
  - Multicolumn：布尔类型，设置列表框是否为多列显示，默认值false
  - SelectionMode：设定列表框选择属性（不允许选择、允许选择一项、允许选择多项）
  - SelectedItem：列表框中当前选定项（单项）
  - SelectedItems：列表框中当前选定项（多项）
  - SelectedIndex：列表框中当前选定项的索引
- 事件：
  - SelectedIndexChanged：用户改变列表选定项时，触发此事件
- 方法：
  - Items.Add(Item)：把一个列表项加入列表框的底部
  - Items.Insert(Index,Item)：把一个列表项插入到列表框的指定索引位置
  - Items.Remove(Item)：清除列表框中的指定列表项
  - Items.Clear()：清除所有列表项

#### 6.3.7 CheckedListBox：可选列表框

同列表框，区别在于其每个列表项的左侧显示选择框

#### 6.3.8 ComboBox：组合框/下拉框

- 组合框提供了一个供选择的列表框，若用户选中列表框中某个列表项，该列表项的内容将自动装入文本框中。当列表框中没有所需的选项时，也允许在文本框中直接输入特定的信息
- 属性：
  - DropDownStyle：设置组合框的样式
    - Simple：无下拉列表框，不能选择，可以输入
    - DropDown：（默认）有下拉列表框，也可以输入
    - DropDownList：有下拉列表框，但不能输入
- 其它属性和事件同列表框

#### 6.3.9 Panel：面板

- 容器控件，可以容纳其它控件，同时为控件分组
- 属性：
  - BorderStyle：设置边框样式（可选无边框，使窗体分区更美观）
  - AutoScroll：布尔类型，设置是否在框内加滚动条

#### 6.3.10 GroupBox：分组框

- 容器控件，可以容纳其它控件，同时为控件分组
- 属性：
  - Text：显示标题

#### 6.3.11 ScrollBar：滚动条

- 分为HScrollBar（水平滚动条）和VScrollBar（垂直滚动条）
- 属性：
  - Value：滚动条滑块位置代表的值
  - Minimum、Maximum：滚动条极限位置的Value
  - SmallChange：单击滚动条两端箭头时，滑块移动的增量值
  - LargeChange：单击滚动条空白处时，滑块移动的增量值
- 事件：
  - Scroll：鼠标或键盘移动滚动条滑块时，触发该事件
  - ValueChanged：通过Scroll事件或以编程方式更改Value时，触发该事件

#### 6.3.12 Timer：定时器

- 定时器是按一定时间间隔周期性自动触发事件的控件，程序运行时定时器不可见
- 属性：
  - Enable：布尔类型，值为true时启动定时器
  - InterVal：引发定时器事件的时间间隔，以ms为单位
- 方法：
  - Start、Stop：启动、停止定时器
- 事件：
  - Tick：按一定时间间隔周期性自动触发的事件

#### 6.3.13 TreeView：显示分级信息

- TreeView控件可以显示树形目录，显示具有层次结构的信息
- 节点对象（Node）与节点集合（Nodes）

  - 每项信息都有一个与之关联的Node对象
  - 每个Node对象都有唯一的索引，treeView1.Nodes[0]表示根节点
  - node1.Text为对象node1的标签文本
  - TreeView控件和每个Node均有属性Nodes，表示其所有子节点（下一级的节点）构成的集合
- 属性：

  - LabelEdit：布尔类型，指示用户是否可以自行编辑节点的标签文本，默认值false
  - TopNode：获取视图控件中第一个完全可见的树节点
  - SelectedNode：获取选中的Node对象
- 方法：

  - 为选定节点加入子节点：SelectedNode.Nodes.Add(待加入的新节点)方法
  - 为选定节点加入兄弟节点：SelectedNode.Parent.Nodes.Add(待加入的新节点)
  - 删除选定节点：SelectedNode.Remove()

    （要求选定节点没有下一级节点，判断方法：检查SelectedNode.Nodes.Count是否为0）
  - 展开选定节点的所有子节点：SelectedNode.ExpandAll()

    （先令SelectedNode=treeView1.Nodes[0]，可展开TreeView控件上的所有节点）
  - 展开选定节点的下一级节点：SelectedNode.Expand()
  - 折叠选定节点的所有子节点：SelectedNode.Collapse()
- 事件：

  - BeforeLabelEdit：编辑树节点标签文本前发生
  - AfterLableEdit：编辑树节点标签文本后发生
  - AfterSelect：选定树节点标签文本后发生
  - AfterExpand：在展开树节点后发生

#### 6.3.14 ListView：显示项目列表视图

- ListView控件可按列表的形式显示数据
- 属性：
  - View：数据的显示模式
  - MultiSelect：布尔类型，表示是否允许多选
  - SelectedItems：用于获取选定的项

#### 6.3.15 MenuStrip：主菜单

- 主菜单通常显示在窗体的最上方
- 包含4种不同类型的菜单项：
  - MenuItem：菜单项，可包含子菜单项
  - ComboBox：下拉菜单
  - TextBox：文本框
  - Separator：菜单项分隔符
- 不同菜单项使用不同的事件进行处理：
  - MenuItem：常用Click事件
  - ComboBox：常用SelectedIndexChanged事件
  - TextBox：常用TextChanged事件

#### 6.3.16 ContextMenuStrip：上下文（右键）菜单

- 添加过程：
  - 在工具箱中添加上下文菜单contextMenu1
  - 对上下文菜单的菜单项进行编辑
  - 将准备使用该上下文菜单的控件的ContextMenuStrip属性更改为contextMenu1，使得控件与上下文菜单相关联

#### 6.3.17 ToolStrip：工具栏

- 工具栏需要依靠在窗体上，其形态类似于主菜单，但功能更为复杂

#### 6.3.18 StatusStrip：状态栏

- 其形态类似于主菜单和工具栏，通常置于窗体的最下方，在其中使用Label控件展示一些状态信息

### 6.4 鼠标事件处理

- 通过窗体的事件MouseMove读取鼠标当前位置
- 通过窗体的事件MouseDown判断是哪个鼠标按键被按下

```C#
//用2个文本框显示鼠标指针在窗体上移动时，鼠标指标所指的位置
实现代码如下：
private void Form1_MouseMove(object sender, MouseEventArgs e)
{
    //txtX、txtY是两个显示鼠标坐标的文本框
     this.txtX.Text = Convert.ToString(e.X);
     this.txtY.Text = Convert.ToString(e.Y);
}

//判定鼠标按键
private void Form1_MouseDown(object sender, MouseEventArgs e)
{
     if (e.Button == MouseButtons.Left)
         MessageBox.Show("按动鼠标左键！");
     if (e.Button == MouseButtons.Middle)
         MessageBox.Show("按动鼠标中键！");
     if (e.Button == MouseButtons.Right)
          MessageBox.Show("按动鼠标右键！");
}
```

### 6.5 键盘事件处理

- 相关的事件：KeyDown、KeyUp、KeyPress
- KeyDown和KeyUp具有属性KeyCode，记录按键对应的编码，适用于几乎所有按键
- KeyPress具有属性KeyChar，记录按键对应的ASCII码，适用于对应有ASCII码的按键
- KeyPress具有属性Handled，为布尔类型，记录是否处理过KeyPress事件

```C#
//例一：实现显示所按动的按键名称。
private void Form1_KeyUp(object sender, KeyEventArgs e)
{
     MessageBox.Show("你所按动的键为：" + e.KeyCode.ToString());
}

//例二：只允许输入数字、退格和回车的文本框
private void txtProduceNum_KeyPress(object sender, KeyPressEventArgs e)
{
      if ((e.KeyChar != 8 && !char.IsDigit(e.KeyChar))
         && e.KeyChar != 13)
      {
          MessageBox.Show("只能输入数字");
          e.Handled = true;//表示已经处理过KeyPress事件
      }
}
```

### 6.6 窗体之间的数据交互

- 窗体A通过读写窗体B的属性、窗体B中控件的属性，将数据传递到窗体B
- 当窗体A已实例化、窗体B还未实例化时，窗体A通过对窗体B进行实例化，并在实例化时附带参数，将数据传递到窗体B

### 6.7 通用对话框

#### 6.7.1 OpenFileDialog：打开文件对话框

- 使用方法：

```C#
//打开文件对话框是一个名为OpenFileDialog的类，打开文件对话框前需先创建该类的实例，再调用该类的ShowDialog()方法
OpenFileDialog ofd=new OpenFileDialog();

//设置属性
ofd.InitialDirectory = "F:\\文档";
ofd.Filter = "王浩雄文件(*.whx)|*.whx|All files (*.*)|*.*";


//当打开文件对话框选定文件时，ShowDialog()方法返回DialogResult.OK；当取消操作时，ShowDialog()方法返回DialogResult.Cancel
if (ofd.ShowDialog() == DialogResult.OK) 
{
    MessageBox.Show("选中的文件名是"+ofd.FileName);		//执行操作相关代码
}
else MessageBox.Show("用户取消操作");
```

- 属性：
  - InitialDirectory：设定打开文件对话框要显示的初始目录
  - Filter：设置过滤文件字符串
  - Title：设置对话框标题
  - Multiselect：布尔类型，控制是否允许多选文件，默认值false
  - FileName：单选文件时，被选中文件的绝对路径（是打开文件对话框的最终输出结果）
  - SafeFileNames：string[]类型，多选文件时，被选中文件的绝对路径

#### 6.7.2 SaveFileDialog：保存文件对话框

使用方法和属性同打开文件对话框

#### 6.7.3 FolderBrowserDialog：文件夹浏览对话框

使用方法同打开文件对话框，属性有不同：

- 属性：

  - Description：用于描述对话框
  - RootFolder：设定打开对话框要显示的初始目录

    ```C#
    //默认值：Environment.SpecialFolder.Desktop（用户的桌面目录）
    ```
  - SelectedPath：被选中文件夹的绝对路径（是文件夹浏览对话框的最终输出结果）

#### 6.7.4 FontDialog：字体设置对话框

- 使用方法：

  ```C#
  //使用前，需先将FontDialog控件在工具箱中拖到当前程序中
  //字体设置对话框是一个名为FontDialog的类，打开字体设置对话框前需先创建该类的实例，再调用该类的ShowDialog()方法
  
  FontDialog fd=new FontDialog();
  
  //设置属性


  //当完成操作时，ShowDialog()方法返回DialogResult.OK；当取消操作时，ShowDialog()方法返回DialogResult.Cancel
  if (fd.ShowDialog() == DialogResult.OK) 
  {
      //选定的字体：fd.Font
      //选定的颜色：fd.Color
  }
  else MessageBox.Show("用户取消操作");
  ```

- 属性：

  - ShowColor：布尔类型，控制是否允许在对话框中选择颜色，默认值false
  - ShowApply：布尔类型，控制是否显示“应用”按钮，默认值false
  - Font与Color：字体设置对话框的最终输出结果

  ```C#
  //提取Font中的各种成分
  textBox1.Text = fontDialog1.Font.Bold.ToString();
  textBox1.Text += fontDialog1.Font.Name;
  textBox1.Text += fontDialog1.Font.Style.ToString();
  textBox1.Text += fontDialog1.Font.Size.ToString();
  textBox1.Text += fontDialog1.Font.GdiCharSet.ToString();
  ```

- 事件：

  - Apply：当显示“应用”按钮且按下该按钮时，激发该事件

#### 6.7.5 ColorDialog：颜色设置对话框

使用方法和属性同字体设置对话框

#### 6.7.6 MessageBox.Show()方法：消息对话框

```C#
MessageBox.Show("消息内容","消息标题（可选）",参数buttons（可选）,参数icon（可选）);
```

```C#
//例：
if (MessageBox.Show("你要去参观上海世博会吗？", "上海世博会", MessageBoxButtons.YesNo) == DialogResult.Yes)
{
    //相应处理的代码
}
```

## 第七章：图形程序设计

### 7.1 绘图坐标系


### 7.2 Graphics对象

- 进行图形处理，需先创建Graphics类的对象，并用该对象的方法进行图形处理
- 创建Graphics对象的方法

  - 在窗体或控件的Paint事件中直接引用Graphics对象（用于在新的窗体或控件上绘图）

    ```C#
      Private void Form_Paint(object sender,System.Windows.Forms.PaintEventArgs e)
      {   Graphics g = e.Graphics;
        ...
      }
      //每个窗体或控件都有Paint事件，其参数e包含了当前窗体或控件的Graphics对象，可直接引用
    ```

    - 利用窗体或控件的CreateGraphics方法（用于在已存在的窗体或控件上绘图）

      ```C#
      Graphics g = this.CreateGraphics();
      //该对象g表示this这个控件或窗体的绘图表面
      ```
  - 从图像对象创建Graphics对象（用于更改已存在的图像）

    ```C#
    Bitmap  bitmap = new Bitmap(@”C:\test\a1.bmp”);
    Graphics g = Graphics.FromImage( bitmap );
    ```

- Graphics类的常用属性

| 属性名称           | 说 明                                                            |
| ------------------ | ---------------------------------------------------------------- |
| CompositingMode    | 获取一个值，该值指定如何将合成图像绘制到此Graphics类             |
| CompositingQuality | 获取或设置绘制到此Graphics类的合成图像的呈现质量                 |
| DpiX               | 获取此Graphics类的水平分辨率                                     |
| DpiY               | 获取此Graphics类的垂直分辨率                                     |
| InterpolationMode  | 获取或设置与此Graphics类关联的插补模式                           |
| IsClipEmpty        | 获取一个值，该值指示此Graphics类的剪辑区域是否为空               |
| IsVisibleClipEmpty | 获取一个值，该值指示此Graphics类的可见剪辑区域是否为空           |
| PageScale          | 获取或设置此Graphics类的全局单位和页单位之间的比例               |
| PageUnit           | 获取或设置用于此Graphics类中的页坐标的度量单位                   |
| PixelOffsetMode    | 获取或设置一个值，该值指定在呈现此Graphics类的过程中像素如何偏移 |
| RenderingOrigin    | 为抵色处理和阴影画笔获取或设置此Graphics类的呈现原点             |
| SmoothingMode      | 获取或设置此Graphics类的呈现质量                                 |
| TextContrast       | 获取或设置呈现文本的灰度校正值                                   |
| TextRenderingHint  | 获取或设置与此Graphics类关联的文本的呈现模式                     |
| Transform          | 获取或设置此Graphics类的几何图形变换的副本                       |
| VisibleClipBounds  | 获取此Graphics类的可见剪辑区域的边框                             |

- Graphics类的常用方法

| 方法名称        | 说 明                                                                    |
| --------------- | ------------------------------------------------------------------------ |
| BeginContainer  | 保存具有此Graphics类的当前状态的图形容器，然后打开并使用新的图形容器     |
| Clear           | 清除整个绘图面并以指定背景色填充                                         |
| Dispose         | 释放由Graphics类使用的所有资源                                           |
| DrawArc         | 绘制一段弧线，它表示由一对坐标、宽度和高度指定的椭圆部分                 |
| DrawBezier      | 绘制由4个Point结构定义的贝塞尔样条                                       |
| DrawBeziers     | 用Point结构数组绘制一系列贝塞尔样条                                      |
| DrawClosedCurve | 绘制由Point结构的数组定义的闭合基数样条                                  |
| DrawCurve       | 绘制经过一组指定的Point结构的基数样条                                    |
| DrawEllipse     | 绘制一个由边框（该边框由一对坐标、高度和宽度指定）定义的椭圆             |
| DrawIcon        | 在指定坐标处绘制由指定的Icon表示的图像                                   |
| DrawImage       | 在指定位置并且按原始大小绘制指定的Image                                  |
| DrawLine        | 绘制一条连接由坐标对指定的两个点的线条                                   |
| DrawLines       | 绘制一系列连接一组Point结构的线段                                        |
| DrawPie         | 绘制一个扇形，该形状由一个坐标对、宽度、高度以及两条射线所指定的椭圆定义 |
| DrawPolygon     | 绘制由一组Point结构定义的多边形                                          |
| DrawRectangle   | 绘制由坐标对、宽度和高度指定的矩形                                       |
| DrawString      | 在指定位置并且用指定的Brush和Font对象绘制指定的文本字符串                |
| FillRectangle   | 填充由一对坐标、一个宽度和一个高度指定的矩形的内部                       |
| Flush           | 强制执行所有挂起的图形操作并立即返回而不等待操作完成                     |

### 7.3 其它常用的对象

- 常与Graphics类一同使用的对象

| 对象名称 | 说 明                    |
| -------- | ------------------------ |
| Pen      | 画笔，绘制线条、形状轮廓 |
| Brush    | 画刷，填充图形区域       |
| Font     | 字体                     |
| Color    | 颜色                     |

#### 7.3.1 颜色

- 颜色使用Color对象进行记录
- 创建颜色对象的方法：

  - 直接指定RGB值和透明度值

    ```C#
    //法一：指定R、G、B三色
    Color myColor=Color.FromArgb(255,0,0);
    //法二：指定透明度和R、G、B三色
    Color myColor=Color.FromArgb(255,255,0,0);
    
    A：透明度（255表示完全不透明）
    R：红色
    G：绿色
    B：蓝色
    ```

  - 使用系统预定义颜色

    ```C#
    Color myColor=Color.Red;
    ```

#### 7.3.2 画笔

- 构造函数的重载：

  ```C#
  Pen(Color color);	//指定画笔颜色
  Pen(Color color,float width);	//指定画笔颜色和宽度
  Pen(Brush brush);	//通过已存在的画笔对象创建画笔
  Pen(Brush brush,float width);	//通过已存在的画笔对象创建画笔，并指定宽度
  ```

- Pen对象的属性：

  - Color：颜色
  - Width：宽度
  - DashStyle：线形
  - StartCap：线头形状
  - EndCap：线尾形状

    ```C#
    pen.DashStyle = DashStyle.Dot;//修改线形为点划线
    pen.StartCap = LineCap.Flat;
    pen.EndCap = LineCap.ArrowAnchor;//修改线头、线尾形状，使之呈箭头形
    ```

#### 7.3.3 画刷

- 几种不同类别的画刷：

  |                     |                          |
  | ------------------- | ------------------------ |
  | SolidBrush          | 纯色填充                 |
  | HatchBrush          | 使用预设图案填充         |
  | TextureBrush        | 使用图像纹理填充         |
  | LinearGradientBrush | 使用渐变色填充           |
  | PathGradientBrush   | 使用复合的混合色渐变填充 |

- 构造函数的重载：

  ```C#
  SolidBrush(Color color);
  
  HatchBrush(预设图案,Color 前景色,Color 背景色);
  
  TextureBrush( Image )
  TextureBrush( Image, Rectangle )
  TextureBrush( Image, WrapMode ) 
  TextureBrush( Image, Rectangle, ImageAttributes)
  TextureBrush( Image, WrapMode, Rectangle)
  /*
  Image：用于指定画笔的填充图案。
  Rectangle：用于指定图像上用于画笔的矩形区域，其位置不能超越图像的范围。
  WrapMode：WrapMode枚举成员用于指定如何排布图像，可以是
      Clamp       完全由绘制对象的边框决定
      Tile        平铺
      TileFlipX   水平方向翻转并平铺图像
      TileFlipY   垂直方向翻转并平铺图像
      TileFlipXY  水平和垂直方向翻转并平铺图像
  例：TextureBrush myBrush = new TextureBrush(new Bitmap(@"e:\test\m23.jpg"));
  */
  
  LinearGradientBrush(this.ClientRectangle,Color 颜色1,Color 颜色2，LinearGradientMode.Vertical);
  ```

#### 7.3.4 字体

- 构造函数

  ```C#
  Font(string 字体名称,字体大小,样式);
  
  样式：
  Bold 粗体
  Italic 斜体
  Regular 常规
  Strikeout 删除线
  Underline 下划线
  ```

### 7.4  Graphics对象的方法

#### 7.4.1 平移、缩放、旋转

```C#
TranslateTransform(float 平移的X分量,float 平移的Y分量);
RotateTransform(float 旋转角度);	//相对原点进行旋转
ScaleTransform(float X方向缩放比例,float Y方向缩放比例);
```

#### 7.4.2 画直线

- DrawLine方法（指定两个点，画一条线段）

  ```C#
  DrawLine(Pen pen,int x1,int y1,int x2,int y2);
  ```
  
- DrawLines方法（指定多个点，画多条线段）

  ```C#
  DrawLine(Pen pen,Point[] pts);
  
  //其中，Point[]为点组成的结构体数组，Point为表示点的结构体，每个点具有x和y两个属性，表示横纵坐标
  
  //例：
  private void Form1_Paint(object sender,System.Windows.Forms.PaintEventArgs e)
  {	Pen pen = new Pen(Color.Black,3);
  	Point[] points ={ 
       new Point(10,10),
       new Point(10, 100),
       new Point(200,50),
       new Point(250,120)
      };
  	e.Graphics.DrawLines(pen, points);   
  }
  ```

#### 7.4.3 画椭圆

```C#
DrawEllipse(Pen pen, int x, int y, int width, int height)
FillEllipse(Brush brush, int x, int y, int width, int height)
//其中x, y为椭圆外接矩形左上角的坐标，width定义椭圆的外接矩形的宽度,height定义椭圆外接矩形的高度
  
DrawEllipse(Pen pen, Rectangle rect)
FillEllipse(Brush brush, Rectangle rect)
//其中rect为Rectangle结构，用于确定椭圆的外接矩形
```

#### 7.4.4 画圆弧、扇形

```C#
//画圆弧
DrawArc( Pen pen, int x, int y, int width, int height, 
int  startAngle, int sweepAngle );

//画扇形
DrawPie( Pen pen, int x, int y, int width, int height, int  startAngle, int sweepAngle );
FillPie( Brush brush, int x, int y, int width, int height ,int startAngle, int sweepAngle );


//x, y为椭圆外接矩形左上角的坐标
//width定义椭圆的外接矩形的宽度
//height定义椭圆外接矩形的高
//startAngle圆弧起点
//sweepAngle顺时针画过的角度
```

#### 7.4.5 画矩形

- DrawRectangle、FillRectangle方法（画一个矩形）

```C#
DrawRectangle(Pen pen, int x, int y, int width, int height);
FillRectangle( Brush brush, int x, int y, int width,int height );

DrawRectangle(Pen pen, Rectangle rect)
FillRectangle( Brush brush, Rectangle rect );

//其中rect为Rectangle结构
    Rectangle rect = new Rectangle(x1,y1,x2,y2);
```

- DrawRectangles方法（画多个矩形）

```C#
DrawRectangles( Pen pen, Rectangle[] rects )
```

#### 7.4.6 画贝塞尔曲线

- 画贝塞尔曲线至少需给定四个点：起始点、终止点和两个控制曲线形状的点
- 给定四个点时，使用DrawBezier方法；给定多于四个点时，使用DrawBeziers方法

```C#
DrawBezier( Pen pen, float x1, float y1, float x2,float  y2, float x3, float y3, float x4, float y4 );
  
DrawBezier( Pen pen, Point pt1, Point pt2, Point pt3, Point pt4 );

DrawBeziers( Pen pen, Point[ ]  points )
```

#### 7.4.7 画多边形

```C#
DrawPolygon( Pen pen, Point [ ] points );
DrawPolygon( Pen pen, PointF [ ] points );
//其中：PointF为Point结构体的float数据类型形式

//例:画一个四边形
private void button_Click(object sender, System.EventArgs e )
{
   Graphics  g = this.CreateGraphics( );
   Pen  pen = new Pen( Color.Red, 2 );
   g.Clear( this.BackColor );
   Point[ ]  p1 = new Point[]{  
       new Point( 10, 120 ),  
       new Point( 120, 100),
       new Point( 300,180 ), 
       new Point( 60, 200) 
   };
   g.DrawPolygon( pen, p1 );
}
```

#### 7.4.8 画闭合曲线、开放曲线

```C#
//画闭合曲线
DrawClosedCurve( Pen pen, Point[ ] pts );
DrawClosedCurve( Pen pen, PointF[ ] pts );

//画开放曲线
DrawCurve( Pen pen, Point[ ] pts );
DrawCurve( Pen pen, PointF[ ] pts );
```

#### 7.4.9 画整个路径的各个对象

使用DrawPath方法（略）

#### 7.4.10 文本输出

```C#
DrawString(String string,Font font,Brush brush)
```

#### 7.4.11 绘制图像

```C#
Bitmap myBitmap = new Bitmap("C:\\boy.jpg");
Graphics g = pictureBox1.CreateGraphics();
g.DrawImage(myBitmap, 0, 0);
```

## 第八章：Web应用开发
