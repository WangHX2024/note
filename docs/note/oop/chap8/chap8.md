# Chapter 8: Operator Overloading

## 一、运算符重载的概念

### 1. 支持重载的运算符

```cpp
// 以下运算符可被重载
+ - * / % ^ & | ~
= < > += -= *= /= %=
^= &= |= << >> >>= <<= ==
!= <= >= ! && || ++ --
, ->* -> () []
new new[]
delete delete[]

// 以下运算符不可被重载
. .* :: ?:
sizeof typeid
static_cast dynamic_cast const_cast reinterpret_cast
```

### 2. 运算符重载的规律和限制

- 不能创建新的运算符
- 运算符重载后，操作数的个数不变
- 运算符重载后，运算符的优先级不变

## 二、运算符重载的形式

### 1. 以成员函数形式重载运算符

```cpp
class Integer
{
public:
	Integer(int n = 0): i(n) {};
	Integer operator+(const Integer& n) const{
		return Integer(i + n.i);
	}
private:
	int i;
}
```

- 特点：可对第二个变量进行自动类型转换，不对第一个变量进行自动类型转换

```cpp
Integer x(1), y(5), z;
z = x + y;    // 合法
z = x + 3;    // 合法，自动由 3 构造 Integer 类的对象
z = 3 + y;    // 不合法，3 不会转换为 Integer 类的对象
```

- 对于二元运算符，重载函数接收一个参数；对于一元运算符，重载函数不接收参数

```cpp
Integer operator-() const{
	return Integer(-i);
}
```

### 2. 以全局函数形式重载运算符

```cpp
class Integer
{
public:
	friend Integer operator+(const Integer&, const Integer&);
private:
	int i;
};

Integer operator+(const Integer& lhs, const Integer& rhs)
{
	return Integer(lhs.i + rhs.i);
}
```

- 特点：可对第一个和第二个变量进行自动类型转换

```cpp
Integer x(1), y(5), z;
z = x + 3;    // 合法，自动由 3 构造 Integer 类的对象
z = 3 + y;    // 合法，自动由 3 构造 Integer 类的对象
```

- 问题：重载函数内部若访问对象的私有字段，需将该重载函数定义为该类的 `friend` ，或使用权限为 `public` 的接口
- 对于二元运算符，重载函数接收两个参数；对于一元运算符，重载函数接收一个参数

## 三、运算符重载的参数和返回类型

### 1. 参数传递

- 如果重载函数不修改参数中的对象，则应当传入常量引用
- 以成员函数形式重载运算符时，如果重载函数不修改当前对象，则应当声明为 `const`
    - `+,-` 等算数运算符、 `>,<` 等比较运算符声明为 `const`
    - `=,++,--` 等赋值运算符不声明为 `const`

### 2. 返回类型

- `+,-` 等算数运算符：返回一个新的对象
- `>,<` 等比较运算符：返回 `bool` 类型
- 索引运算符 `[]`：返回引用

## 四、运算符重载的实现

### 1. 自增 / 自减运算符 `++ / --`

```cpp
Integer& Integer::operator++() {
	this->i +=1 ;
	return *this
}

// the int argument is not used so leave it unnamed
Integer Integer::operator++(int){
	Integer old(*this);
	++(*this);
	return old;
}
```

- 前缀类型（Prefix）： `++i`
    - 参数表为空
    - 返回类型为对象的引用
- 后缀类型（Postfix）： `i++`
    - 参数表为一个 `int` 类型的值，编译器为其自动传入 `0`
    - 返回类型为一个新的对象（因为原对象已经被修改，所以不能返回原对象的引用）

### 2. 比较运算符

```cpp
bool Integer::operator==( const Integer& rhs ) const {
	return i == rhs.i;
}

// 在实现新的比较运算符时，可复用已实现的比较运算符
bool Integer::operator!=( const Integer& rhs ) const {
	return !(*this == rhs)
}
```

### 3. 索引运算符 `[]`

```cpp
class Vector{
public:
	int& operator[]( int index ){ return a[index]; }
	...
private:
	int a[3];
}

int main(){
	Vector v(100);
	v[0] = 1;
}
```

- 索引运算符必须是类的成员
- 只能接收一个参数
- 返回引用类型，以方便使用其它代码对其进行修改

### 4. 括号运算符 `()`

```cpp
struct F{
	void operator()(int x) const {
	std::cout<< x << std::endl;	
};

F f;
f(2);    // 像函数一样调用
```

- 对括号运算符重载，可以形如函数地使用对象，又称为 Functor

## 五、类型转换 Type Conversions

编译器会在下述情形执行自动类型转换（implicit conversions）：

- 存在单参数构造函数
- 存在类型转换运算符（type conversion operator）

### 1. 单参数构造函数

```cpp
class PathName{
	string name;
public:
	PathName();
	PathName(const string&);
};

string abc("abc");
PathName xyz;
xyz = abc;    // 发生从 string 到 PathName 的自动类型转换，因为 PathName 存在单参数构造函数，且参数类型匹配
```

- 使用 `explicit` 修饰单参数构造函数，从而阻止使用该构造函数进行自动类型转换

```cpp
class PathName{
	...
	explicit PathName(const string&);
};

string abc("abc");
PathName xyz;
xyz = abc;    // 发生错误，自动类型转换被阻止
```

### 2. 类型转换运算符

```cpp
class Rational {
public:
	operator double() const{
		return numerator / (double)denominator;
	}
}

Rational r(1,3);
double d = 1.3 * r;    // r 自动转换为 double 类型
```

- 通用形式：将 X 类型转化为 T 类型 `X::operator T() {...}`
- 类型转换运算符会在需要时被自动调用
- 不需指定返回类型，返回类型与函数名相同
- 不存在参数