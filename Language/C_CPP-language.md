# C/C++ Language

Tags : C/C++

---

## 名词

### accessor and mutator
* accessor即C++中类成员的 get 方法, mutator即 set 方法.
* 不将成员变量直接暴露, 而是通过get/set方法使得变量的访问可控, 可调试.

### const and constexpr
* `const`：大致意思是说我承诺不改变这个值，主要用于说明接口，这样变量传递给函数就不担心变量会在函数内被修改了编译器负责确认并执行const的承诺。 
* `constexpr`：大致意思是在编译时求值，主要用于说明常量，作用是允许数据置于只读内存以及提升性能。
    * `constexpr` 定义函数:
    
    ```C++
    constexpr int Inc(int i) {
        return i + 1;
    }
    ```
    * `constexpr` 定义类构造函数: 如果提供给该构造函数的参数都是constexpr, 那么产生的对象中的所有成员都会是constexpr, 该对象也就是constexpr对象, 可用于各种只能使用constexpr的场合. 构造函数函数体必须为空.
    
    ```C++
    struct A {
        constexpr A(int xx, int yy): x(xx), y(yy) {}
        int x, y;
    };
    ```

### dynamic initialization and static initialization(动态初始化与静态初始化)
* 动态初始化是指初始化时有些non-trivial操作, 比如分配内存, 获取线程ID等. 否则是静态初始化.
* 静态生命周期的对象总是先执行静态初始化(0或常量), 再根据需要执行动态初始化. 静态初始化分两种:
    * zero initialization(零初始化): 初始化为0
    * constant initialization(常量初始化): 初始化为常量表达式
    * 具有[静态存储周期](#static storage duration(静态存储周期))的变量存储在data段或bss段
        * data段存储的是用常量表达式初始化的变量
        * bss段是未初始化的变量, 这部分变量在装载时分配空间, 并进行零初始化. 程序运行时在调用构造函数进行动态初始化

### static storage duration(静态存储周期)
* 具有静态存储周期的对象, 生命周期从其初始化开始一直持续到程序结束.
* 全局变量(定义在 namespace scope 内的变量), 静态变量(类静态变量, 函数静态变量)都是静态存储周期对象.

### template metaprogramming(模板元编程)
* 指以一类技术, 用模板语法写与类型相关的程序, 并且执行于编译时.
* 优点: 提供类型安全高效的模板 
* 缺点:
    * 模板本身代码可读性低, 难于debug和维护
    * 编译时错误信息复杂难懂
    * 不利于代码重构

### trivial destructor
* 析构函数啥事也不需要干的类, 称为 trivially destructible. 比如基础类型(int, pointers, ...), trivially destructible类型的array 或 constexpr 修饰的变量.
* 析构函数需要干点事的类, 称为 non-trivially destructible. 比如std::string.

### unnamed namespace and static(匿名名字空间与Static)
* 匿名名字空间内可以自定义类型, static无法修饰.
* static修饰的符号是修改了符号的bind属性, 使其只在当前文件有效. 匿名名字空间其实是给名字空间起了个独一无二的名字, 符号本身还是具有外部链接属性.

---

## 特殊用法

### 用ASCII字符串输出非ASCII字符
使用utf-8编码([UTF-8在线编解码](https://mothereff.in/utf-8)). 比如汉字 `仙`, 它的utf-8编码是3个字节, 值分别为 0xE4, 0xBB, 0x99, 可以使用 `printf("\xE4\xBB\x99")` 输出显示.

---

## 注意点

### C调用约定 `__stdcall` 与 `__cdecl`
* name mangling
    * gcc(x86/x64)和msvc(x64)上都是原函数名, 不做decoration. 只有msvc(x86)会为 `__stdcall` 函数改名, `foo(xxx)` 生成的symbol为 `_foo@(一个数字)`.
    * 运行时加载动态库需要特殊处理. 
* 行为方式不同:
    * `__stdcall` 在函数内处理栈, 适用于定义一般API函数和Callback函数, 因为各编译器对栈的处理方式不同, 不宜将这部分工作丢给调用者.
    * `__cdecl` 调用者处理栈, 适用于定义可变参数的函数.

