# Lect 3: STL

## 一、概念

1. 标准模板库（Standard Template Library，STL），是 ISO C++ 标准库的一部分，包含各种数据结构和算法
2. STL 的组成部分：容器（Containers）、算法（Algorithms）、迭代器（Iterator）
3. **容器的分类**
    1. Sequential：array、vector、deque（双头队列）、forward_list（单向链表）、list（双向链表）
    2. Associative：set（collection of unique keys）、map（collection of key-value maps）、multiset、multimap
    3. Unordered Associative：unordered_set、unordered_map、unordered_multiset、unordered_multimap
    4. Adaptors：stack、queue、priority_queue

## 二、Vector

1. **概述**
    - `vector` 是一种**泛型类**（Generic Class）。这种类需要指定两种类型，其中一个是容器自身的类型（这里是 `vector`），另一个是容器内元素的类型（上例中就是 `int`）
    - `vector` 的内部空间可按需扩大：当有更多项被放入时，它就会为这些项提供足够的空间
    - `vector` 会记录当前保存的项数，可以用 `size()` 方法读取
    - `vector` 内部项的顺序即为项的插入顺序，因此可按相同的顺序检索
2. **构造函数（Constructors）**
    - `vector<Elem> c;`
    - `vector<Elem> c1(c2);`
3. **获取大小**
    - `V.size()`：获取当前容器内项数（C++ 11 前为线性时间）
    - `V.empty()`：是否为空，相比 `.size()` 速度更快（常数时间）
    - `V.capacity()`：返回当前分配的容量可以存放的元素数
    - `V.reverse(size_t n)`：预留至少 n 个元素的存储空间
    - `V.resize(size_t n)`：将容器的项数调整为 n
4. **迭代器**
    - `V.begin()`：获取指向第一个位置的迭代器
    - `V.end()`：获取指向最后一个位置的迭代器
    - `V.cbegin()`：获取指向第一个位置的常量迭代器（不能用于修改元素，更安全）
    - `V.cend()`：获取指向最后一个位置的常量迭代器
5. **元素访问**
    - `V.at(index)`：该方法会进行边界检查，如果越界，编译器会抛出异常，更加安全
    - `V[index]`：该方法不会做边界检查，如果越界的话，则行为不可预测，是未定义的行为（Undefined Behaviour），因此速度快但不安全
    - `V.front()`：获取第一个元素的引用
    - `V.back()`：获取最后一个元素的引用
    
    ```cpp
    int main()
    { 
    	list<string> s; 
    	s.push_back("hello"); 
    	s.push_back("world"); 
    	list<string>::iterator p;
    	for(p = s.begin(); p != s.end(); p++) 
    	cout << *p <<" ";
    }
    ```
    
6. **添加 / 删除 / 查找**
    - `V.push_back(e)`
    - `V.pop_back()`
    - `V.insert(pos, e)`，其中 `pos` 是迭代器变量
    - `V.clear()`：清空向量内所有元素
    - `find(first, last, item)`，其中 `first`、`last` 是迭代器变量，返回的是位于 `first` 和 `last` 之间的迭代器，如果没有找到的话则返回 `last`
    - `V.erase(pos)` ：删除指定位置的元素，其中 `pos` 是迭代器变量
7. **其他**
    - 支持比较运算符： `== != < > <= >=`
    - `V.swap(v2)`：交换 `V` 和 `v2`

## 三、List

1. **操作**
    
    ```cpp
    
    x.front()
    x.back()
    x.push_back(item)
    x.push_front(item)
    x.pop_back()
    x.pop_front()
    x.erase(pos1, pos2)
    x.count()
    x.reverse(size)
    x.resize()
    ```
    
2. 列表元素大小不确定，因此使用迭代器对列表遍历时，只能使用 `==` 或 `!=` 比较运算符
3. C++ 无法为列表预留空间，所以列表没有 `capacity()` 函数

## 四、Map

1. **映射**（Maps）是一种关联容器（类似 Python 中的字典），用于存储由**键**（Keys）及其映射值构成的元素，以特定顺序排列
2. 键常用于排序或识别唯一的元素，映射值存储对应键的内容
3. 可用 `[]` 运算符，通过键来访问映射值
4. 使用 `[]` 访问不存在的键，就会创建一个新的键，为此可以使用 `count()` 或 `contain()` 进行访问
    
    ```cpp
    if(food.count("apple"))
    if(food.contains("apple")) // introduced in C++ 20
    ```
    

## 五、Stack

1. Stack 在 STL 中体现出了 “Adapter” 的思想，即利用一些已有的模板添加上一些属于 Stack 的特性（即 Adapter），最后封装成为了栈模块