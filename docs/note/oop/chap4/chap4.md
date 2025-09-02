# Chapter 4: Memory Model

## 一、变量

1. **变量的存放位置**
    - 存放在 Stack 中的数据：Local Vars（局部变量）
    - 存放在 Heap 中的数据：Dynamically Allocated Vars（由 `new` `malloc` 等动态分配的变量）
    - 存放在 Code / Data 区中的数据：Global Vars、Static Global Vars、Static Local Vars（全局变量、静态全局和局部变量）

![image.png](image.png)

1. **全局变量**
    - 在一个 .cpp 文件内定义为全局变量 / 函数后，在另一个 .cpp 文件内使用时，需使用 `extern` 关键字； `extern` 关键字告知编译器该变量 / 函数已在其它位置定义
    - 全局变量的构造函数在 `main` 函数运行前被调用
2. **静态变量 Static**
    - **静态全局变量**阻止来自本 .cpp 文件以外的访问
    - **静态局部变量**在不同的函数调用之前保持值的不变，其构造函数的调用发生于它的第一次访问之时

## 二、指针与引用

### 1. 指针 Pointer

```cpp
// 指针的定义
string s = "hello";
string* ps;

// 指针的赋值
ps = &s;

// 使用指针获取对象
(*ps).length();

// 使用指针调用对象的方法
ps->length();
```

### 2. 引用 Reference

1. 引用相当于为原变量起一个别名，在使用上与原变量差别不大
2. 引用必须在初始化时完成与原变量的绑定，此后不能修改绑定关系
    
    ```cpp
    char c;
    
    // 定义指针
    char* p = &c;
    
    // 直接定义引用
    char& r = c;
    
    // 在函数的参数表中定义引用，当相应的函数被调用时，引用进行初始化
    void f (int& x);
    f(y);
    ```
    
3. 非 `const` 类型的引用，绑定的对象必须是左值（Lvalue）
    
    ```cpp
    void f (int& x);
    f (i * 3);    // 该句会报错，因为 (i * 3) 是右值
    ```
    
4. 没有指向引用的引用，因为引用和引用的引用都指向原变量
5. 没有指向引用的指针，但可以有指向指针的引用
    
    ```cpp
    int&* p;            // illegal
    void f(int*& p);    // OK
    ```
    
6. 指针与引用的比较
    
    
    | **Pointer** | **Reference** |
    | --- | --- |
    | 独立于绑定的对象，可以不进行初始化 | 依赖于绑定的对象，必须进行初始化 |
    | 可以修改绑定的对象 | 不可修改绑定的对象 |
    | 可以设置为 `NULL` | 不可设置为 `NULL` |

## 三、动态分配内存

1. `new` 用于分配内存空间并返回一个指针，该指针是访问这一块内存空间的唯一方式，与 `malloc` 相对应
2. `delete` 用于将内存空间回收到内存池，与 `free` 相对应
3. `new` 和 `delete` 可以保证构造函数 / 析构函数的正确调用，而 `malloc` 和 `free` 不调用构造函数 / 析构函数
4. `new` 和 `delete` 是运算符，而 `malloc` 和 `free` 是函数
5. `new` 和 `delete` ，`malloc` 和 `free` 需要成对使用，不能混搭
6. 不要对同一内存空间使用多次 `delete`
7. 对空指针 `NULL` 使用 `delete` 是安全的（无事发生）

```cpp
int* psome = new int [10];
delete[] psome;
```

## 四、常量 Const

1. 由 `const` 修饰的变量称为常量
2. 常量必须在初始化时完成赋值，一旦完成初始化就不能修改
3. **常量的内存空间**
    - 编译器尽力不为常量分配内存空间，因此在某一 .cpp 文件中定义的常量无法在另一 .cpp 文件中访问
    - 若需为常量分配内存空间并支持在其它文件访问，需在定义和访问常量处都使用 `extern` 关键字
4. **常量的分类**
    - 按照常量值得以确定的时间，常量可分为 **编译时常量**（Compile-time Constants）和 **运行时常量**（Run-time Constants）
    - 编译时常量可以用于数组下标；运行时常量不可用于数组下标
    
    ```cpp
    // 编译时常量
    const int class_size = 12;
    int finalGrade[class_size];    // OK
    
    // 运行时常量
    int x;
    cin >> x;
    const int size = x;
    double classAverage[size];     // illegal
    ```
    
5. **常量与函数**
    - 若函数的参数含有常量，则参数在函数体内不能进行修改
    - 若函数的返回值为常量，则返回值在函数体内必须指定为常量
    
    ```cpp
    void f1 (const int i)
    {
    	i++;    // illegal, const value cannot be modified
    }
    
    const int f2()
    {
    	return 1;  // The return value have to be a constant
    }
    int k = f2();
    k++;    // legal
    
    ```
    
6. **常量与指针**
    - `const string* p = &s` 或 `string const* p = &s`
        - 这里 `const` 修饰的是 `string`，即 `p` 指向一个 `const string`
        - 不能通过 `p` 修改 `s`，但 `p` 本身可以指向其他 `string`
    - `string *const p = &s;`
        - 这里 `const` 修饰的是 `p`，表示 `p` 是一个 `const` 指针，但指向的 `string` 可以修改
        - 不能修改 `p` 的指向，但可以修改 `s` 的值
    
    ```cpp
    const string* p = &s;
    string const* p = &s;
    string *const p = &s;
    ```
    
    ```cpp
    // 示例
    int i = 1;
    const int ci = 3;
    int* ip;
    const int* cip;
    
    ip = &ci;  // 非法：ip 是指向 int 类型的可修改指针，这样将导致 const int 类型可能被修改，因此编译器会报错
    cip = &ci; // 合法
    
    ip = &i;   // 合法
    cip = &i;  // 合法
    
    *ip = 54;  // 合法
    *cip = 54; // 非法，无论 cip 指向的是 int 或是 const int
    ```
    
7. **常量与引用**
    - `const string& p = s`
        - 这里 `const` 修饰的是 `string`，即 `p` 引用的是一个 `const string`
        - 不能通过 `p` 修改 `s`