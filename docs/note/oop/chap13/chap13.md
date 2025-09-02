# Chapter 13: Smart Pointers

### 1. 智能指针的思想来源

- **RAII：**C++ 中一种强大且被广泛应用的编程技术。其核心思想是将资源的生命周期与对象的生命周期绑定：资源获取发生在对象的构造阶段，资源释放发生在对象的析构阶段
- 由于资源在析构过程自动释放，因此可以将指针作为某个特殊对象的成员，当该对象的生命周期结束时，自动调用析构函数，对指针指向的内存空间进行释放，从而降低因忘记 `delete` 而导致的内存泄漏风险
- 这样的 “特殊对象” 即称为 **智能指针**；为便于使用，这个 “特殊对象” 在使用方法上需要与一般的指针相似

### 2. 唯一指针 `std::unique_ptr`

- 独占所有权：`std::unique_ptr` 对其指向的对象拥有唯一的、排他的所有权，即只有一个 `std::unique_ptr` 实例可以指向并负责管理特定的动态内存
- 不可复制，但可以移动：
    - 为了保证所有权的唯一性，`std::unique_ptr` 不支持拷贝操作（即拷贝构造函数和拷贝赋值运算符被禁用）
    - 唯一指针支持移动操作（`std::move`），允许将所有权从一个唯一指针 A 转移到另一个唯一指针 B；当所有权转移后，唯一指针 A 不再指向该对象，唯一指针 B 原来指向的内存空间将被销毁

```cpp
#include <iostream>
#include <memory>

struct MyData {
    int value;
    MyData(int v) : value(v) {}
    void print() const {
        std::cout << "Value: " << value << std::endl;
    }
};

int main() {
    std::unique_ptr<MyData> u_ptr1(10); // 创建 unique_ptr
    u_ptr1->print(); // 通过 -> 访问成员
    // std::unique_ptr<MyData> u_ptr2 = u_ptr1; // 编译错误：unique_ptr 不可复制
    std::unique_ptr<MyData> u_ptr3 = std::move(u_ptr1); // 转移所有权，u_ptr1 现在为空
}
```

### 3. 共享指针 `std::shared_ptr`

- 共享所有权：`std::shared_ptr` 允许多个实例共同指向并拥有同一个动态分配的对象。它内部通过 **引用计数**（Reference Count）机制来跟踪有多少个 `std::shared_ptr` 实例正共享该对象
- 引用计数：
    - 当一个新的 `std::shared_ptr` 指向该对象（例如通过拷贝构造或赋值），引用计数会增加
    - 当一个 `std::shared_ptr` 被销毁或不再指向该对象时，引用计数会减少
    - 通过共享指针的 `use_count()` 方法查看该共享指针指向对象的引用计数
- 自动销毁：只有当最后一个指向对象的 `std::shared_ptr` 被销毁，使得引用计数降为零时，该对象才会被自动销毁

```cpp
#include <iostream>
#include <memory>
#include <vector>

struct SharedResource {
    int id;
    SharedResource(int i) : id(i) {}
};

int main() {
    std::shared_ptr<SharedResource> s_ptr1(101);  // 创建 shared_ptr
    std::cout << "s_ptr1 use_count: " << s_ptr1.use_count() << std::endl; // 输出 1

    std::shared_ptr<SharedResource> s_ptr2 = s_ptr1; // 拷贝构造，引用计数增加
    std::cout << "s_ptr1 use_count: " << s_ptr1.use_count() << std::endl; // 输出 2
    std::cout << "s_ptr2 use_count: " << s_ptr2.use_count() << std::endl; // 输出 2

    std::vector<std::shared_ptr<SharedResource>> ptr_vector;
    ptr_vector.push_back(s_ptr1);
    ptr_vector.push_back(s_ptr2);
    ptr_vector.push_back(std::make_shared<SharedResource>(202));

    std::cout << "s_ptr1 use_count after vector push: " << s_ptr1.use_count() << std::endl; // 输出 4 (s_ptr1, s_ptr2, vector[0], vector[1])
    std::cout << "ptr_vector[2] use_count: " << ptr_vector[2].use_count() << std::endl; // 输出 1

    s_ptr1.reset(); // s_ptr1 不再指向对象，引用计数减少
    std::cout << "After s_ptr1.reset(), s_ptr2 use_count: " << s_ptr2.use_count() << std::endl; // 输出 3

    ptr_vector.clear(); // vector 中的 shared_ptr 被销毁，引用计数相应减少
    std::cout << "After vector.clear(), s_ptr2 use_count: " << s_ptr2.use_count() << std::endl; // 输出 1

    // s_ptr2 在 main 函数结束时离开作用域，引用计数变为 0，SharedResource(101) 被销毁
    // SharedResource(202) 在 ptr_vector.clear() 后引用计数变为 0 并被销毁
    return 0;
}
```