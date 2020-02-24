# C/C++ Language

Tags : C/C++

---

## 注意点

### C调用约定 `__stdcall` 与 `__cdecl`
* name mangling
    * gcc(x86/x64)和msvc(x64)上都是原函数名, 不做decoration. 只有msvc(x86)会改名, `__stdcall` 的函数 `foo(xxx)` 生成的symbol为 `_foo@(一个数字)`, `__cdecl` 的函数 `foo(xxx)` 生成的symbol为 `foo`.
    * 运行时加载动态库需要特殊处理. 
* 行为方式不同:
    * `__stdcall` 在函数内处理栈, 适用于定义一般API函数和Callback函数, 因为各编译器对栈的处理方式不同, 不宜将这部分工作丢给调用者.
    * `__cdecl` 调用者处理栈, 适用于定义可变参数的函数.



