# Lect 1-2: Introduction

## 一、字符串

### 1. 字符串的构造

```cpp
// 构造函数
string (const char *cp, int len);
string (const string& s2, int pos); // 使用常量引用是为了避免传值带来的拷贝开销
string (const string& s2, int pos, int len);

// 示例
// 用C风格字符串初始化
string str1="Hello World!";

// 用构造函数初始化
string str2=string("Hello World!");

// 从str1的第6位开始，向后取5个字符，构造新字符串，即str3="World"
string str3=string(str1,6,5);
// 这个构造函数的重载形式如下，其中
string(const string& s2,int pos,int len)

// 初始化包含5个'A'的字符串
string str4=string(5,'A');
```

### 2. 字符串的方法

1. **连接：利用运算符重载**
    
    ```cpp
    str=str1+str2;
    str+="Hello";
    ```
    
2. **获取长度：length 方法**
    
    ```cpp
    int len=str1.length();
    ```
    
3. **赋值：assign 方法**
    
    ```cpp
    // 格式
    assign (const string& str); //string 
    assign (const string& str, size_t subpos, size_t sublen); //substring 
    assign (const char* str); //C-string 
    assign (const char* str, size_t n); //buffer 
    assign (int n, char c); //fill
    // 示例
    str1.assign(10,'A');// 令str1="AAAAAAAAAA"（对原字符串进行修改）
    ```
    
4. **插入：insert 方法**
    
    ```cpp
    // 格式
    insert (int pos, const string& str);
    insert (int pos, const string& str, int subpos, int sublen); 
    insert (int pos, const char* str); 
    insert (int pos, const char* str, int n); 
    insert (int pos, int n, char c);
    // 示例
    str1.insert(7, "World");  // 在位置7 **之前** 插入"World"（对原字符串进行修改）
    ```
    
5. **在末尾插入：append 方法**
    
    ```cpp
    // 格式
    append (const string& str);
    append (const char* s);
    // 示例
    str.append("World!");  // 在末尾追加 "World!"（对原字符串进行修改）
    ```
    
6. **部分删除：erase 方法**
    
    ```cpp
    // 格式
    erase (int pos = 0, int len = npos); // 默认参数删除字符串内的所有字符
    // 示例
    str1.erase(7,5);  // 删除从位置7开始的5个字符（对原字符串进行修改）
    ```
    
7. **查找子字符串：find 方法**
    
     `find` 从 `pos` 开始查找字符串 `str`, 返回第一次匹配的第一个字符的位置
    
    ```cpp
    // 格式
    find (const string& str, int pos = 0);
    // 示例
    str_to_find="hangzhou";
    str2="He is in hangzhou";
    int pos=str2.find(str_to_find); // 查找子字符串的出现位置，即pos=9
    ```
    
8. **取子字符串：substr 方法**
    
    `substr` 拷贝字符串从 `pos` 位置开始的 `len` 个字符
    
    - 如果 `pos` 超出了字符串长度，那么会产生异常
    - 如果 `pos` 等于字符串长度，那么会得到空字符串
    - 如果 `pos + len` 超出了字符串长度，那么只会拷贝到字符串末尾
    
    ```cpp
    // 格式
    substr (int pos, int len);
    // 示例
    str3=str2.substr(9,8);// str3为从str2的第9位开始，向后取8位得到的子字符串（原字符串不变
    ```
    
9. **部分替换：replace 方法**
    
    `replace` 代替从 `pos` 开始 `len` 的字符串
    
    ```cpp
    // 格式
    replace (int pos, int len, const string& str);
    replace (int pos, int len, const string& str, int subpos, int sublen); 
    replace (int pos, int len, const char* str); 
    replace (int pos, int len, const char* str, int n); 
    replace (int pos, int len, int n, char c);
    str2.replace(9,8,"beijing");//将str2的第9位开始，向后取8位字符的得到的子字符串替换为"beijing"（对原字符串进行修改）
    ```
    

## 二、文件输入输出流

```cpp
#include<fstream>   // 文件输入输出流
using namespace std;

int main()
{
		// 使用构造函数，构造ofstream类的对象fout，以把内容输出到文件"out.txt"
		ofstream fout("out.txt");
		fout<<"Hello World!"<<endl;
		
		// 使用构造函数，构造ifstream类的对象fin，以从文件"in.txt"读入内容
		ifstream fin("in.txt");
		fin>>str1>>str2;
}
```