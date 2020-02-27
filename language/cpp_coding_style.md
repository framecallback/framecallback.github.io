# C++ 代码规范 - QGC

Tags : C++

---

## 原则

* 加强代码可读性, 提高代码可维护性.
* 禁用一些危险的语言特性, 提高可靠性.
* 禁用一些tricky用法, 提高可维护性.
* 优化性能时有时会与规范订立的约束条款相冲突, 适当突破规则.

---

## 参考

* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
* [google/styleguide repo](https://github.com/google/styleguide)
* [Qt Coding Style](https://wiki.qt.io/Qt_Coding_Style)
* [Qt Coding Conventions](https://wiki.qt.io/Coding_Conventions)

---

## 格式

名词:

* **camel case**: 每个单词首字母大写. 缩略词不要用全大写, 也用首字母大写. 数字间隔可以用下划线. 如 `class Protocol8_0`, `enum ProjectErrors`.
* **lower case**: 每个字母都小写, 单词中间用一个下划线 `_` 分隔. 如 `file_name`.
* **upper case**: 每个字母都大写, 单词中间用一个下划线 `_` 分隔. 如 `FILE_NAME`.

### 文件命名

* 头文件以 `*.h` 命名, 源文件以 `*.cpp` 命名. 通常头文件与源文件名配套.
* 文件名由小写字母, 下划线 `_`组成.
* 不要使用 "/usr/include/" 目录下已经存在的文件名, 如 "db.h".
* 文件命名特殊化一些比较好, "http\_server\_logs.h" 好于 "logs.h".

例如, 类名为 `FooBar` 的类的头文件可以命名为 `foo_bar.h`, 源文件可以命名为 `foo_bar.cpp`.

### 文件编码

* 所有文件使用UTF-8无BOM格式编码.
* 文件内只允许使用ASCII字符, 包括注释.
* 必须使用非ASCII字符时, 使用UTF-8编码. ([UTF-8在线编解码](https://mothereff.in/utf-8))
* 禁止使用C++的 `char16_t` 和 `char32_t`.

### 缩进
* 使用2个空格.
* 预处理宏的 `#` 必须顶格写, 嵌套时 `#` 后可以使用空格缩进.
* namespace不缩进. namespace嵌套时, 每个namespace放一行, 都不缩进.

### 命名
* **类型名**:
    * 使用 camel case;
    * 包括 class, struct, enum, type alias, type template parameter.
* **变量名**:
    * 要意义明确, 不要使用短名字和缩写, 除非约定的counters或temporaries;
    * 普通变量名和struct成员变量名使用 lower case;
    * 类成员变量也使用 lower case, 额外追加一个下划线后缀. 如 `file_map_`.
* **常量**: 使用 `k` 前缀, camel case. 如 `const int kAndroid8_0_0 = 24;`.
* **函数**: 使用 camel case, 首字母大写, get/set方法也是如此.
* **namespace**:
    * 全小写. 最上级namespace名字根据项目名称取;
    * nested namespace取名不要取通用的名字, 如 `util` 等.
* **枚举**: 使用常量命名方式, 避免宏冲突. 如 `kOk = 0, kErrorUnknown = -1`.
* **宏**: 使用 upper case.
* **特例**: 如果使用的名字是模仿现有的C/C++语言或库功能, 使用已有的命名方式.

### 注释
* 一律使用 `//`.
* 行尾注释在 `//` 前空2个空格.
* **文件注释**:
    * 头文件和源文件都要包含License和版权声明, 不要包含作者;
    * 需要对文件功能说明的时候, 可以写在头文件注释部分.

```C++
// Copyright 2019 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//      https://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
//
// (file comment here) Additional definitions for internal users of the api. 
// This should only be included from internal implementation files.
```
* **类注释**:
    * 功能复杂的类需要提供注释来说明类的作用及其用法:
    
    ```C++
    // Iterates over the contents of a GargantuanTable.
    // Example:
    //    GargantuanTableIterator* iter = table->NewIterator();
    //    for (iter->Seek("foo"); !iter->done(); iter->Next()) {
    //      process(iter->key(), iter->value());
    //    }
    //    delete iter;
    class GargantuanTableIterator {
      ...
    };
    ```
* **函数注释**:
    * 功能复杂的函数要提供注释来说明函数的作用及其用法;
    * 使用 indicative mood ("Opens the file"), 不要使用 imperative ("Open the file").
* namespace 以注释结束. `//` 前面空2个空格.

```c++
namespace A {

...

}  // namespace A
```

### 变量声明
* 值类型和指针类型分开声明, 不放在一行.
* 在声明时初始化, 不要分两行. 如 `int i = f();` 好于 `int i; i = f();`
* 变量到需要使用的时候再定义, 不要提前定义.

### 换行
* 当 `if` 语句体只有一个语句时允许单行 `if (foo) return xxx;`, 其它不允许复合语句写在一行.
* 类成员函数实现在头文件中且只有一个语句时允许单行. `int size() const { return vector_.size(); }`
* 每行不超过80字符, 除非拆了实在影响阅读代码, 比如用了长URL.
* 换行时, 运算符放在行首

```C++
if (longExpression
    + otherLongExpression
    + otherOtherLongExpression) {
}
```

### 空行
* 可以用空行来分隔代码段.
* 最多使用一个空行.

### 空格
* 指针 `*` 和引用 `&`, 与type之间隔一个空格, 与变量名之间空格

```C++
char *x;
const std::string &myString;
const char * const y = "hello";
```
* 二元运算符左右各留一个空格.
* 逗号后面留一个空格.
* 行末禁止留空格.

示例:

```C++
void f(bool b) {  // Open braces should always have a space before them.
  ...
int i = 0;  // Semicolons usually have no space before them.
// No spaces inside braces for braced-init-list.
int x[] = {0};

// Spaces around the colon in inheritance and initializer lists.
class Foo : public Bar {
 public:
  // For inline function implementations, put spaces between the braces
  // and the implementation itself.
  Foo(int b) : Bar(), baz_(b) {}  // No spaces inside empty braces.
  void Reset() { baz_ = 0; }  // Spaces separating braces from implementation.
  ...
```

循环语句与条件语句示例:

```C++
if (b) {          // Space after the keyword in conditions and loops.
} else {          // Spaces around else.
}
while (test) {}   // There is usually no space inside parentheses.
switch (i) {
for (int i = 0; i < 5; ++i) {
// Range-based for loops always have a space before and after the colon.
for (auto x : counts) {
  ...
}
switch (i) {
  case 1:         // No space before colon in a switch case.
    ...
  case 2: break;  // Use a space after a colon if there's code after it.
```

运算符示例:

```C++
// Assignment operators always have spaces around them.
x = 0;

// Other binary operators usually have spaces around them. 
// Parentheses should have no internal padding.
v = w * x + y / z;
v = w * (x + z);

// No spaces separating unary operators and their arguments.
x = -5;
++x;
if (x && !y)
  ...
```

模板与类型转换示例:

```C++
// No spaces inside the angle brackets (< and >), before
// <, or between >( in a cast
std::vector<std::string> x;
y = static_cast<char*>(x);
```

### 括号
* 左大括号不换行; 如果右大括号后面有其它关键字, 放在同一行.
* 不管循环体, 条件语句体有几行语句, 都使用花括号.
* 循环体内没有语句时, 允许花括号放在同一行. `while (1) {}`.
* 使用小括号分组表达式, 提高可读性. `(a + b) & c`, `if ((a && b) || c)`.

### switch语句
* `case` 语句缩进.
* 对于不 `break` 或 `return` 的case语句, 如果不为空, 使用注释 `// FALL THROUGH` 提示进入下一个case.

### 跳转指令
* 跳转指令后面不要使用 `else` 语句:

```C++
// Wrong
if (foo) {
    return;
} else {
    somethingElse();
}

// Correct
if (foo) {
    return;
}
somethingElse();
```

### #define Guard
格式为 `<PROJECT>_<PATH>_<FILE>_H_`.

```c++
#ifndef FOO_BAR_BAZ_H_
#define FOO_BAR_BAZ_H_

...

#endif  // FOO_BAR_BAZ_H_
```

### #include顺序
* 对应头文件, C系统头文件, C++系统头文件, 其它库头文件和当前项目库头文件.
* 分组中间以单个空行隔开. 组内按字母顺序排列. 

```C++
// dir2/foo2.h.

// C system headers (headers in angle brackets with the .h extension), e.g.:
// #include <unistd.h>
// #include <stdlib.h>

// C++ standard library headers (without file extension), e.g.:
// #include <algorithm>
// #include <cstddef>

// Other libraries' .h files.
// Your project's .h files.

// Conditional includes, such as
// #ifdef __cplusplus
// #include <memory>
// #endif
```

### 函数

* **参数**:
    * 参数列表排序: 输入参数 -> 输入输出参数 -> 输出参数;
    * 参数要写变量名, 除非明显没用也再不会用的参数, 如 `A(const A&) = delete`;
    * 参数列表过长时, 换行参数与第一个参数对齐. 如果第一个参数就过长了, 4空格indent:
    
    ```C++
    ReturnType LongClassName::ReallyReallyReallyLongFunctionName(
        Type par_name1,  // 4 space indent
        Type par_name2,
        Type par_name3) {
      DoSomething();
      ...
    }
    ```

### 类
* **声明顺序**:
    * 一律 public -> protected -> private;
    * `public`, `protected` 和 `private` 关键字用1个空格缩进;
    * 每一个section内按相似性分组, 顺序为: types(typedef, using, nested structs and classes) -> constants -> factory functions -> constructors -> assignment operators -> destructor -> all other methods -> data members.

类声明示例:

```C++
class MyClass : public OtherClass {
 public:      // Note the 1 space indent!
  MyClass();  // Regular 2 space indent.
  explicit MyClass(int var);
  ~MyClass() {}

  void SomeFunction();
  void SomeFunctionThatDoesNothing() {}

  void set_some_var(int var) { some_var_ = var; }
  int some_var() const { return some_var_; }

 private:
  bool SomeInternalFunction();

  int some_var_;
  int some_other_var_;
};
```

类初始化列表示例:

```C++
// When everything fits on one line:
MyClass::MyClass(int var) : some_var_(var) {
  DoSomething();
}

// If the signature and initializer list are not all on one line,
// you must wrap before the colon and indent 4 spaces:
MyClass::MyClass(int var)
    : some_var_(var), some_other_var_(var + 1) {
  DoSomething();
}

// When the list spans multiple lines, put each member on its own line
// and align them:
MyClass::MyClass(int var)
    : some_var_(var),             // 4 space indent
      some_other_var_(var + 1) {  // lined up
  DoSomething();
}

// As with any other code block, the close curly can be on the same
// line as the open curly, if it fits.
MyClass::MyClass(int var)
    : some_var_(var) {}
```

---

## 规范

### 头文件

* 原则上每个.cpp文件都应该对应一个.h文件, 除非unittests或只包含一个 `main()` 函数.
* **自包含**: 头文件应该include所有它本身依赖的其它头文件. 模板类的实现, 和inline函数的实现, 都放在声明所在的同一个头文件内, 不要另起文件.
* **前置声明**: 避免使用前置声明, 直接 #include 其头文件.
* **inline函数**:
    * 只在函数少于10行时声明为inline函数. 注意析构函数通常比看起来要长不少, 因为有隐含的调用;
    * 通常递归函数不用inline.

### Namespace
* 通常情况下, 代码要放入namespace. namespace命名要基于项目名.
* 禁止使用 using-directive (e.g. `using namespace std;`).
* 禁止使用 inline namespace.
* 禁止在 `std` namespace里面添加任何东西.
* 头文件里禁止使用 namespace aliases, 除非internal-only作用域内, 比如函数内, internal namespace内.
* 源文件内部使用的变量/函数/类等, 放入unnamed namespace内, 替代 `static`.

```C++
namespace {

...

}  // namespace
```

### 非成员函数与静态成员函数
* 尽量不要暴露非成员函数在头文件里, 即尽量让所有的函数都应该是成员函数或静态成员函数.
* 通常跨类的二元运算符重载会使用非成员函数.

### 局部变量
* if和while需要使用的局部变量定义放在语句内. `while (const char* p = strchr(str, '/')) str = p + 1;`. 除非变量需要反复调用构造函数和系够函数, 可定义在循环体外提高效率.

### 静态变量和全局变量
* **静态存储周期变量** 分为静态变量和全局变量; **静态变量**又分为静态非局部变量和 静态局部变量. **静态非局部变量** 包括 **静态全局变量** 和 **静态类成员变量**, **静态局部变量** 指函数内静态变量.
* 静态存储周期变量必须是trivial destructible, 即: 基础类型(int, pointers, ...), trivially destructible类型的array 或 constexpr 修饰的变量.
* 静态非局部变量和全局变量的初始化只允许零初始化, 常量表达式初始化, 或确保初始化不会受顺序影响的初始化, 比如 `int p = getpid();`.
* 静态局部变量允许使用动态初始化.
* 常用:
    * 常字符串使用 `const char*` , 而非 `std::string`;
    * Maps, sets 以及其它动态容器不可作为静态存储周期变量, 如必须使用, 使用静态局部变量;
    * 禁止使用智能指针作为静态存储周期变量;
    * 实在不行, 可以使用普通指针或引用类型的静态局部变量, 不用释放.

### thread\_local变量
* C++11支持 `thread_local Foo foo = ...`来定义TLS变量, 只允许这种方式来定义.
* thread\_local变量只允许静态初始化, 不允许动态初始化.

### class(类)

* **构造函数**: 构造函数中禁止调用虚函数, 禁止构造函数内存在可能导致构造失败的指令.
* **隐式类型转换**: 禁止定义隐式类型转换. 类型转换方法和单参数构造函数都必须加 `explicit`, 除非拷贝构造函数, 移动构造函数, 和 使用 `std::initialize_list` 的构造函数.
* **拷贝和移动构造函数**: 每个类public部分应该写明该类支持的拷贝/移动构造函数, 除非显而易见:
    * 没有private部分的类(如struct, interface-only基类);
    * 基类不可拷贝/移动.
* **Struct**:
    * 大部分情况都使用class, 只在包裹纯数据时使用struct, 或像STL里一样用在无状态类型里, 如traits, template metafunctions, functors等;
    * struct可以有设置数据的方法, 如构造函数, 析构函数, Init(), Reset();
    * 尽量使用struct替代pair和tuple, 可读性强.
* **继承**:
    * 禁止继承自模板类, 有内存泄漏, 符号重名等问题;
    * Composition(组合)通常比Inheritance(继承)好, 如果使用继承, 必须是public;
    * 重写虚函数时使用 `override` 替代使用 `virtual`;
    * 多重继承时只允许一个基类是非接口类, 其它的都要是接口类;
    * 不要覆盖基类的虚函数, 使用 `using BaseClass::Foo;` 暴露基类的虚函数.
* **运算符重载**:
    * 定义运算符重载需语义明确, 遵从习惯用法;
    * 避免使用模板函数来重载运算符;
    * 如果重载运算符, 要重载整套相关的, 如 `<` 相关的是所有比较运算符.
* **成员变量**一律private, 除非constant可以public.
* **friend(友元)**: friend的对象通常定义在同一个文件内.

### 函数

* **输入参数** 通常为value或const引用, **输出参数** 和 **输入输出参数** 用指针.
* 函数体不宜太长, 功能单一, 实现简短比较好.
* 所有左值引用必须是const的. 输入参数尽量用左值引用, 除非需要nullptr.
* **函数重载**的前提是一眼就能看出用户选择的是哪个函数, 比如重载函数的参数类型不同, 参数个数不同等.
* **默认参数**: 虚函数禁止使用默认参数.
* **Trailing Return Type(尾置返回类型)**: 通常只允许用在lambda表达式中, 或在模板中能使代码更可读, 如
```
template <typename T, typename U>
auto add(T t, U u) -> decltype(t + u);
```
替代
```
template <typename T, typename U>
decltype(declval<T&>() + declval<U&>()) add(T t, U u);
```
* **lambda表达式**: 捕获的参数要在列表里写明, 不要省略.

### 其它特性

* **smart pointer(智能指针)**:
    * 需要智能指针的时候, 尽量使用 `std::unique_ptr`, 非必要情况下不使用 `std::shared_ptr`, 禁止使用 `std::auto_ptr`;
    * 需要控制权转移的时候, 使用 `std::unique_ptr` 作为参数.
* **type deduction(类型推导)**:
    * 只在能使代码更安全更清晰的地方使用;
    * **auto**: 
        * 尽量少用, 本身类型名不长的地方不要用;
        * 只在类型很明显且类型名很长的地方用, 如容器的迭代器 `auto it = myMap.begin()`.
* **rvalue reference(右值引用)**: 没事不要用, 很多人看不懂. 需要做控制权转移的对象, 用 `std::unique_ptr`.
* **exception(异常)**: 禁止使用.
    * 如果依赖库内部使用异常, 在直接调用的地方 catch 异常;
    * `noexcept` 在对性能影响大的地方使用.
* **RTTI(运行时类型识别)**: 禁止使用.
* **cast(类型转换)**:
    * 避免使用C风格的类型转换, 使用C++风格 `static_cast`, `const_cast` or `reinterpret_cast`:
    
    ```C++
    // Wrong
    char* blockOfMemory = (char* ) malloc(data.size());
    
    // Correct
    char *blockOfMemory = reinterpret_cast<char *>(malloc(data.size()));
    ```
    * 使用构造函数替代强制类型转换: `int(myFloat)` 替代 `(int)myFloat`.
* **align(对齐)**: 不同的架构有不同的对齐要求, 强制类型转换时要格外注意.
* **char(字符)**: 有无符号取决于编译器, 需要考虑符号时, 用 `signed char` 和 `unsigned char` 定义.
* **enum(枚举)**:
    * 使用enum定义整数常量, 替代 `static const int` 或 `#define`;
    * 禁止使用64位枚举值, MSVC不支持.
* **integer(整数)**:
    * 使用<cstdint>中的整数( `int32_t`, `int16_t` 等);
    * 只在表示bit时使用 `uint_xx`. 在需要确保非负数时, 接口函数做范围检查, 内部函数使用assertion.
* **float(浮点数)**: 避免使用 `==` 比较浮点数.
* **stream(流)**: 尽量不要用. 使用时也不要使用改变状态的高级功能.
* `i++` 或 `++i` 单独使用, 不要用于赋值.
* 能用 `const` 就用. 使用 `const int *p`, 不要用 `int const *p`.
* 用 `constexpr` 修饰编译期就确定的常量, 以及constexpr辅助类和函数.
* **macro(宏)**:
    * 能少用就少用, 能用C++特性实现的就用C++特性替代;
    * 头文件里尽量避免定义宏, 必须定义时要使用自己项目的专有前缀.
* 使用 `nullptr` 替代 `NULL`, 字符0用 `'\0'`, 不要直接使用数字 `0`.
* `sizeof(var)` 比 `sizeof(type)` 好, 有变量时就用前者, 只有类型时才用后者.
* **Template Metaprogramming(模板元编程)**:
    * 非常审慎地使用, 尽量不要用;
    * 需要编译时检查类型的地方用 `static_assert`.
* **其它禁止事项**:
    
    * 扩展 `std::hash` 支持的类型;
    * 使用 `<ratio>`, `<cfenv>` 或 `<fenv.h>`, `<filesystem>`;
    * 使用 Nonstandard Extensions.



​    



