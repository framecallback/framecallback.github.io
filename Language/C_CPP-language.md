# C/C++ Language

Tags : C/C++

---

## 名词

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

### trivial destructor
* 析构函数啥事也不需要干的类, 称为 trivially destructible. 比如基础类型(int, pointers, ...), trivially destructible类型的array 或 constexpr 修饰的变量.
* 析构函数需要干点事的类, 称为 non-trivially destructible. 比如std::string.


---

## 注意点

### C调用约定 `__stdcall` 与 `__cdecl`
* name mangling
    * gcc(x86/x64)和msvc(x64)上都是原函数名, 不做decoration. 只有msvc(x86)会改名, `__stdcall` 的函数 `foo(xxx)` 生成的symbol为 `_foo@(一个数字)`, `__cdecl` 的函数 `foo(xxx)` 生成的symbol为 `foo`.
    * 运行时加载动态库需要特殊处理. 
* 行为方式不同:
    * `__stdcall` 在函数内处理栈, 适用于定义一般API函数和Callback函数, 因为各编译器对栈的处理方式不同, 不宜将这部分工作丢给调用者.
    * `__cdecl` 调用者处理栈, 适用于定义可变参数的函数.

