# Chapter 10: Templates

## 一、函数重载与默认参数

1. **函数重载与自动类型转换 Overloading & Auto-Casting**
    
    ```cpp
    void print(int i);
    void print(double i);
    
    print('a');      // 调用 void print(int i)，发生自动类型转换
    print(3L);       // 3L 是 long 型，既可以转换为 int，也可以转换为 double，因此出现冲突，编译报错
    
    ```
    
2. **函数的默认参数 Default Arguments**
    - 默认参数必须从参数表的最右侧开始提供
    - 默认参数的插入由编译器完成
    
    ```cpp
    int harpo(int n, int m = 4,int j = 5);    // 合法
    int harpo(int n, int m = 4,int j);        // 不合法
    
    beeps = harpo(2);    // 等同于 harpo(2, 4, 5)
    ```
    

## 二、模版的概念

1. 要义：在类或函数的定义中，使用类别（Type）作为参数
2. 分类
    - 函数模版（Function Template）：例如 sort 函数
    - 类模版（Class Template）：例如 stack、list、queue 等容器

## 三、函数模版

### 1. 函数模版的定义

1. 使用 `template` 关键字定义模版类
    
    ```cpp
    template <class T>
    void swap(T& x, T& y)
    {
    	T temp = x;
    	x = y;
    	y = temp;
    }
    
    template <class T>
    void sort(Vector<T>& arr);
    ```
    
2. `class T` 指定了一个参数化的类型名，该类型名可在以下场合使用：
    - 函数参数的类别
    - 函数体内局部变量的类别
    - 函数返回值的类别

### 2. 函数模版的实例化 Template Instantiation

1. **模版函数（Template Function）** 是函数模版的实例化；编译器会在所需位置根据函数模版与参数类型，生成对应的模版函数
    
    ```cpp
    int i = 3, j = 4;
    swap(i, j);    // 实例化 int 类型的 swap
    
    string s("Hello");
    string t("World");
    swap(s, t);    // 实例化 string 类型的 swap
    ```
    
2. **函数模版的类型推断**
    - 函数模版的传入参数类型必须与参数表完全一致，不支持隐式自动转换
    - 函数模版与一般的同名函数（Regular Functions）按如下规则共存：
        - 优先调用参数类型完全一致的 Regular Function
        - 其次调用参数类型完全一致的函数模版
        - 最后通过隐式类型转换，调用参数类型不完全一致的 Regular Function
    
    ```cpp
    void f(float i, float k);
    
    template <class T>
    void f(T t, T u);
    
    f(1.0f, 2.0f);    // 两个参数都为 float，调用普通函数
    f(1.0, 2.0);      // 两个参数都为 double，调用函数模版
    f(1, 2);          // 两个参数都为 int，调用函数模版
    f(1, 2.0);        // 进行隐式类型转换，将 1、2.0 转换为 1f、2.0f，调用普通函数
    ```
    
    !!! note
    
        在 C++ 中：
        
        - 形如 `2.0f` 的常量为 `float` 类型
        - 形如 `2.0` 的常量为 `double` 类型
    
3. 在调用时，可以显式地指明函数模版的类型
    
    ```cpp
    template <class T>
    void foo(){...}
    
    foo<int>();
    foo<float>();
    ```
    

## 三、类模板

### 1. 类模板的定义

1. 类模版的声明和实现都应放在头文件中
2. 模版可以接收一或多个类型参数
    
    ```cpp
    template <class T>
    class Vector{
    public:
    	Vector(int);
    	~Vector();
    	Vector(const Vector&);
    	Vector& operator=(const Vector&);
    	T& operator[](int);
    	
    private:
    	T* m_elements;
    	int m_size;
    }
    
    Vector<int> v1(100);
    v1[20] = 10;
    ```
    
    ```cpp
    template <class Key, class Value>
    class HashTable{
    	const Value& lookup(const Key&) const;
    	void insert(const Key&, const Value&);
    };
    ```
    
3. 模版可以嵌套，即模版实例可以作为外层模版的类型参数
    
    ```cpp
    Vector < Vector <double> >
    // 一个存储 double 类型的 Vector 的 Vector
    ```
    
4. 支持复杂类型参数
    
    ```cpp
    Vector <int (*) (Vector<double>&, int) >
    // 一个存储某种函数指针的 Vector
    ```
    
5. **非类型模版参数 Non-Type Parameters**
    - 模版可以接收非类型的参数
    - 可以为非类型参数指定默认值
    
    ```cpp
    template <class T, int bounds = 100>
    class FixedVector{
    public:
    	FixedVector();
    	T& operator[](int);
    private:
    	T elements[bounds];    // 固定长度的数组
    };
    
    // Usage
    FixedVector<int, 50> v1;
    FixedVector<int, 10*5> v2;
    FixedVector<int> v3; // => FixedVector<int, 100>
    ```
    
6. **成员模版 Member Templates**
    - 可以在类中为成员声明模版
    
    ```cpp
    template<typename T>
    class complex{
    public:
    	template<class X>
    	complex(const complex<X>&);
    };
    ```
    

### 2. 类模版与继承

1. 类模版可从非模版类继承
    
    ```cpp
    template<class A>
    class Derived: public Base {...}
    // Base 是非模版类
    ```
    
2. 类模版可从类模版继承
    
    ```cpp
    template<class A>
    class Derived: public List<A> {...}
    // List<A> 是类模版
    ```
    
3. 非模版类可从实例化的类模板继承
    
    ```cpp
    class Supervisor: public List<Employee*> {...}
    // List<Employee*> 是实例化的类模版
    ```
    

### 3. CRTP

CRTP 全称 **奇异递归模版模式（Curiosly Recurring Template Pattern）**，通过在基类模板中使用派生类作为模板参数，实现编译期多态

```cpp
template<class T>
struct Base {
    void interface() {  // 普通成员函数
        static_cast<T*>(this)->implementation();
    }
    
    static void static_func() {  // 静态成员函数
        T::static_sub_func();
    }
};

struct Derived : public Base<Derived> {
    void implementation();
    static void static_sub_func();
};
```

1. **工作原理：普通成员函数模拟虚函数**
    - `Base` 的 `interface()` 方法通过 `static_cast` 将 `this` 指针转换为派生类指针
    - 然后调用派生类的 `implementation()` 方法
    - 这实现了类似虚函数的效果，但没有运行时开销
2. **工作原理：静态成员函数继承**
    - `Base` 的 `static_func()` 直接调用派生类的 `static_sub_func()`
    - 实现了静态多态