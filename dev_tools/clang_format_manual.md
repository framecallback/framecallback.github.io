# clang-format 手册

Tags : C++

---

## 功能

* 自动格式化程序代码.
* 支持语言: C/C++/Java/JavaScript/Objective-C/Protobuf. 新版支持C#.
* 支持代码风格: LLVM, Google, Chromium, Mozilla, WebKit. 新版支持Microsoft.

---

## 安装

### Ubuntu系统

```shell
# Ubuntu16.04上安装的是3.8版本
sudo apt-get install clang-format
```

---

## 项目配置

* **命令行方式**: 使用命令 `clang-format [options] [<file> ...]`, 其中通过 `-style={key: value, ...}` 选项输入自定义的配置.
* **配置文件方式**: 将配置文件 `.clang-format` 放入项目目录. `.clang-format` 可由下面命令创建

```shell
# 创建默认的config文件
clang-format -dump-config > .clang-format

# 创建基于google风格的config文件
clang-format -style=google -dump-config > .clang-format
```

* 可以对指定的代码取消格式化, 只需在前后加上注释 `// clang-format on` 和 `// clang-format off`. 注释本身会被格式化.

```C++
int formatted_code;
// clang-format off
    void    unformatted_code  ;
// clang-format on
void formatted_code_again;
```

---

## 配置说明

### 配置文件说明

* 配置文件使用 YAML 格式.
* 配置文件可以包含多个section, 每个section可以指定不同的语言 `Language`, 每个section之间用 `---` 间隔.
* 第一个section可以不指定语言, 作为所有语言的默认配置. 后续特定语言的配置会覆盖默认配置.

```yaml
# We'll use defaults from the LLVM style, but with 4 columns indentation.
BasedOnStyle: LLVM
IndentWidth: 4
---
Language: Cpp
# Force pointers to the type for C++.
DerivePointerAlignment: false
PointerAlignment: Left
---
Language: JavaScript
# Use 100 columns for JS.
ColumnLimit: 100
---
Language: Proto
# Don't format .proto files.
DisableFormat: true
---
Language: CSharp
# Use 100 columns for C#.
ColumnLimit: 100
...
```

### 配置选项说明(基于3.8版本)

#### Language: Cpp
* 指定语言. None, Cpp, CSharp(新版), Java, JavaScript, ObjC, Proto, TableGen, TextProto.

#### BasedOnStyle: Google
* 基于那个配置文件, Google, LLVM, Chromium, Mozilla, WebKit, Microsoft(新版才有).

#### AccessModifierOffset: -1
* 访问权限关键字 public, protected, private 额外缩进空格数(默认2个空格缩进, -1表示使用2+(-1)=1个空格缩进.

```c++
class A {
 public:
  A();
};
```

#### AlignAfterOpenBracket: Align
* 开括号(开圆括号/开尖括号/开方括号)后的对齐.
    * Align
    * DontAlign
    * AlwaysBreak: 总是在开括号后换行

```c++
// Align
someLongFunction(argument1,
                 argument2);

// DontAlign
someLongFunction(argument1,
    argument2);

// AlwaysBreak
someLongFunction(
    argument1, argument2);
```

#### AlignConsecutiveAssignments: false
* 连续赋值时, 对齐所有等号.

```c++
// false:
int aaaa = 12;
float b = 23;
std::string ccc = 23;

// true:
int aaaa = 12;
int b    = 23;
int ccc  = 23;
```

#### AlignConsecutiveDeclarations: false
* 连续声明时, 对齐所有声明的变量名.

```c++
// false:
int aaaa = 12;
float b = 23;
std::string ccc = 23;

// true:
int         aaaa = 12;
float       b = 23;
std::string ccc = 23;
```

#### AlignEscapedNewlinesLeft: true
* 使用反斜杠换行时的反斜杠尽量向左对齐.

```c++
#define A   \
  int aaaa; \
  int b;    \
  int dddddddddd;
```

#### AlignOperands:   true
* 对齐二元和三元运算符的操作数. 

```c++
int aaa = bbbbbbbbbbbbbbb +
          ccccccccccccccc;
```

#### AlignTrailingComments: true
* 对齐尾置注释.

```c++
// true:
int a;     // My comment a
int b = 2; // comment b

// false:
int a; // My comment a
int b = 2; // comment b
```

#### AllowAllParametersOfDeclarationOnNextLine: true
* 允许函数声明的所有参数在放在下一行.

```c++
// true:
void myFunction(
    int a, int b, int c, int d, int e);

// false:
void myFunction(int a,
                int b,
                int c,
                int d,
                int e);
```

#### AllowShortBlocksOnASingleLine: false
* 允许短的语句块(不包括函数体)放在同一行.

```c++
// false
while (true) {
}
while (true) {
  continue;
}
while (true) continue;  // no effect
int foo(void) { return 0; }  // no effect

// true
while (true) {}
while (true) { continue; }
while (true) continue;  // no effect
int foo(void) { return 0; }  // no effect
```

#### AllowShortCaseLabelsOnASingleLine: false
* 允许短的case标签放在同一行

```c++
// false:
switch (a) {
case 1:
  x = 1;
  break;
case 2:
  return;
}

// true:
switch (a) {
case 1: x = 1; break;
case 2: return;
}
```

#### AllowShortFunctionsOnASingleLine: All
* 允许短的函数放在同一行
    * None
    * InlineOnly: 定义在类中
    * Empty: 空函数
    * Inline: 定义在类中，空函数
    * All

#### AllowShortIfStatementsOnASingleLine: true
* 允许短if单行. `if (a) return;` 可以放到同一行.
* ***新版本使用 Never, WithoutElse, Always***

#### AllowShortLoopsOnASingleLine: true
* 允许短循环语句单行. `while (true) continue;` 可以放到同一行.

#### AlwaysBreakAfterDefinitionReturnType(**deprecated**): None
* 见 *AlwaysBreakAfterReturnType*.

#### AlwaysBreakAfterReturnType: None
* 函数定义中的返回值类型之后是否换行.
    * None
    * All
    * TopLevel: 只在顶层函数换行, 类内忽略.
    * AllDefinitions: 所有函数定义的地方换行, 函数声明的地方不换.
    * TopLevelDefinitions: 只在顶层函数定义的地方换行, 声明不换.

#### AlwaysBreakBeforeMultilineStrings: true
* 多行字符串前面自动换行.

```c++
// true:
const char* str =
    "aaaaaaaa"
    "bbbbbbbb";

// false:
const char* str = "aaaaaaaa"
                  "bbbbbbbb";
```

#### AlwaysBreakTemplateDeclarations: true
* template声明后始终换行.
* ***新版本使用 Yes, No, MultiLine***

```c++
// true:
template <class T>
int foo(T a) {
  return 0;
}

// false:
template <class T> int foo(T a) { return 0; }
```

#### BinPackArguments: true
* 函数调用时的参数是否紧密排列.

```c++
// true:
short_foo(a, b, c);
long_foo(aaaaaaaaaaaaaaaaaaa, bbbbbbbbbbbbbbbbbbb,
         ccccccccccccccccccccccccccccccccc);

// false:
short_foo(a, b, c);
long_foo(aaaaaaaaaaaaaaaaaaaaa,
         bbbbbbbbbbbbbbbbbbbbb,
         ccccccccccccccccccccccccccccccccccc);
```

#### BinPackParameters: true
* 函数声明时的形参是否紧密排列.

```c++
// true:
int short_foo(int a, int b, int c);
void long_foo(int aaaaaaaaaaaaaaaa, int bbbbbbbbbbbbbb,
              int ccccccccccccccccccccccccccccccccc);

// false:
int short_foo(int a, int b, int c);
void long_foo(int aaaaaaaaaaaaaaaa,
              int bbbbbbbbbbbbbb,
              int ccccccccccccccccccccccccccccccccc);
```

#### BraceWrapping:
* 精细控制大括号格式.
* 只在 `BreakBeforeBraces` 设置为 `Custom` 时起作用, 否则忽略.

##### AfterClass:      false

```c++
// false:
class A {
  int a;
};

// true:
class A
{ int a; };
```

##### AfterControlStatement: false

```c++
// false:
if (1) {
  continue;
} else {
  continue;
}

// true:
if (1)
{
  continue;
} else
{ continue; }
```

##### AfterEnum:       false

```c++
// false:
enum Errors {
  kOk = 0,
  kError = -1,
};

// true:
enum Errors
{
  kOk = 0,
  kError = -1,
};
```

##### AfterFunction:   false

```c++
// false:
int foo(void) {
  int a = 1;
  return 0;
}

// true:
int foo(void)
{
  int a = 1;
  return 0;
}
```

##### AfterNamespace:  false

```c++
// false:
namespace a {
int b;
}

// true:
namespace a
{ int b; }
```

##### AfterObjCDeclaration: false
* ObjC 相关.

##### AfterStruct:     false

```c++
// false:
struct foo {
  int x;
};

// true:
struct foo
{
  int x;
};
```

##### AfterUnion:      false

```c++
// false:
union foo {
  int x;
}

// true:
union foo
{
  int x;
}
```

##### BeforeCatch:     false

```c++
// false:
try {
  foo();
} catch () {
}

// true:
try {
  foo();
}
catch () {
}
```

##### BeforeElse:      false

```c++
// false:
if (foo()) {
} else {
}

// true:
if (foo()) {
}
else {
}
```

##### IndentBraces:    false
* 大括号本身缩进.

#### BreakBeforeBinaryOperators: None
* 二元运算符换行方式.
    * None: 在二元运算符后面换行
    * NonAssignment: `=`在后面换行, 其它在运算符前面换行
    * All: 所有二元运算符在符号前面换行

```c++
// None:
LooooooooooongType loooooooooooooooooooooongVariable =
    someLooooooooooooooooongFunction();

bool value = aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa +
                     aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa ==
                 aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa &&
             aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa >
                 ccccccccccccccccccccccccccccccccccccccccc;

// NonAssignment:
LooooooooooongType loooooooooooooooooooooongVariable =
    someLooooooooooooooooongFunction();

bool value = aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                     + aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                 == aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
             && aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                    > ccccccccccccccccccccccccccccccccccccccccc;

// All:
LooooooooooongType loooooooooooooooooooooongVariable
    = someLooooooooooooooooongFunction();

bool value = aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                     + aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                 == aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
             && aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                    > ccccccccccccccccccccccccccccccccccccccccc;
```

#### BreakBeforeBraces: Attach
* 大括号换行风格:
    * **Attach**: Always attach braces to surrounding context.
    * **Linux**: Like Attach, but break before braces on function, namespace and class definitions.
    * **Mozilla**: Like Attach, but break before braces on enum, function, and record definitions.
    * **Stroustrup**: Like Attach, but break before function definitions, catch, and else.
    * **Allman**: Always break before braces.
    * **Whitesmiths**: Like Allman but always indent braces and line up code with braces.
    * **GNU**: Always break before braces and add an extra level of indentation to braces of control statements, not to those of class, function or other definitions.
    * **WebKit**: Like Attach, but break before functions.
    * **Custom**: 自定义风格, 见 `BraceWrapping`.

#### BreakBeforeTernaryOperators: true
* 三元运算符在运算符之前换行.

```c++
// true:
veryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongDescription
    ? firstValue
    : SecondValueVeryVeryVeryVeryLong;

// false:
veryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongDescription ?
    firstValue :
    SecondValueVeryVeryVeryVeryLong;
```

#### BreakConstructorInitializersBeforeComma: false
* 类成员初始化时在逗号前面换行.

```c++
// false:
Aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa::Constructor()
    : initializer00000000000000000000000000000000001(),
      initializer0000000000000000000000002() {}

// true:
Aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa::Constructor()
    : initializer00000000000000000000000000000000001()
    , initializer0000000000000000000000002() {}
```

#### ColumnLimit:     80
* 每行最大长度.
* 0 表示不限长度.

#### CommentPragmas:  '^ IWYU pragma:'
* 描述具有特殊意义的注释的正则表达式，它不应该被分割为多行或以其它方式改变.

#### ConstructorInitializerAllOnOneLineOrOnePerLine: true
* 成员初始化列表要么全放在一行, 要么每个变量一行.

```c++
// true:
SomeClass::Constructor()
    : aaaaaaaa(aaaaaaaa),
      aaaaaaaa(aaaaaaaa),
      aaaaaaaa(aaaaaaaaaaaaaaaaaaaaaaaaa) {
  return 0;

// false:
SomeClass::Constructor()
    : aaaaaaaa(aaaaaaaa), aaaaaaaa(aaaaaaaa),
      aaaaaaaa(aaaaaaaaaaaaaaaaaaaaaaaaa) {
  return 0;
}
```

#### ConstructorInitializerIndentWidth: 4
* 成员初始化列表缩进宽度.

#### ContinuationIndentWidth: 4
* 换行缩进宽度.

#### Cpp11BracedListStyle: true
* 使用C++11的大括号风格.
    * 大括号内侧没有空格
    * 括号内部不换行
    * 使用 *换行缩进* 而非 *block indent*

```c++
// true:                                  
vector<int> x{1, 2, 3, 4};
vector<T> x{{}, {}, {}, {}};
f(MyMap[{composite, key}]);
new int[3]{1, 2, 3};

// false:
vector<int> x{ 1, 2, 3, 4 };
vector<T> x{ {}, {}, {}, {} };
f(MyMap[{ composite, key }]);
new int[3]{ 1, 2, 3 };
```

#### DerivePointerAlignment: true
* 自动分析并使用文件原有的指针符号 `*` 和引用符号 `&` 的对齐方式.

#### DisableFormat:   false
* 关闭格式化功能.

#### ExperimentalAutoDetectBinPacking: false
* 自动分析函数的参数是否一个参数一行.
* ***实验阶段, 不要使用, 风险自负.***

#### ForEachMacros:   [ foreach, Q_FOREACH, BOOST_FOREACH ]
* 列出来的名称会被解释为foreach循环, 而不是函数调用. 格式如下

```c++
FOREACH(<variable-declaration>, ...)
  <loop-body>
```

#### IncludeCategories: 
* include头文件时用空格分成多组, 通过正则表达式和优先级决定组内排序方式. 

```
  - Regex:           '^<.*\.h>'
    Priority:        1
  - Regex:           '^<.*'
    Priority:        2
  - Regex:           '.*'
    Priority:        3
```

#### IndentCaseLabels: true
* case标识符缩进.

```c++
// true:
switch (foo) {
  case 1:

// false:
switch (foo) {
case 1:
```

#### IndentWidth:     2
* 缩进使用空格数.

#### IndentWrappedFunctionNames: false
* 函数名在换行时是否缩进.

```c++
// true:
LoooooooooooooooooooooooooooooooooooooooongReturnType
    LoooooooooooooooooooooooooooooooongFunctionDeclaration();

// false:
LoooooooooooooooooooooooooooooooooooooooongReturnType
LoooooooooooooooooooooooooooooooongFunctionDeclaration();
```

#### KeepEmptyLinesAtTheStartOfBlocks: false
* 语句块开头留一个空行.

```c++
// false:
if (foo) {
  bar();
}

// true:
if (foo) {

  bar();
}
```

#### MacroBlockBegin: ''
* A regular expression matching macros that start a block.

```c++
# With:
MacroBlockBegin: "^NS_MAP_BEGIN|\
NS_TABLE_HEAD$"
MacroBlockEnd: "^\
NS_MAP_END|\
NS_TABLE_.*_END$"

NS_MAP_BEGIN
  foo();
NS_MAP_END

NS_TABLE_HEAD
  bar();
NS_TABLE_FOO_END

# Without:
NS_MAP_BEGIN
foo();
NS_MAP_END

NS_TABLE_HEAD
bar();
NS_TABLE_FOO_END
```

#### MacroBlockEnd:   ''
* A regular expression matching macros that end a block.

#### MaxEmptyLinesToKeep: 1
* 最大连续空行数.

#### NamespaceIndentation: None
* namespace 缩进:
    * None
    * Inner: 只inner namespace缩进
    * All: 所有namespace缩进

```c++
// None:
namespace out {
int i;
namespace in {
int i;
}
}

// Inner:
namespace out {
int i;
namespace in {
  int i;
}
}

// All:
namespace out {
  int i;
  namespace in {
    int i;
  }
}
```

#### ObjCBlockIndentWidth: 2

#### ObjCSpaceAfterProperty: false

#### ObjCSpaceBeforeProtocolList: false

#### PenaltyBreakBeforeFirstCallParameter: 1

#### PenaltyBreakComment: 300

#### PenaltyBreakFirstLessLess: 120

#### PenaltyBreakString: 1000

#### PenaltyExcessCharacter: 1000000

#### PenaltyReturnTypeOnItsOwnLine: 200

#### PointerAlignment: Left
* 指针 `*` 和引用 `&` 的对齐方式:
    * Left: `int* a;`
    * Right: `int *a;`
    * Middle: `int * a;`

#### ReflowComments:  true
* 注释过长时自动重新断行.

```c++
true:
// veryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongComment with plenty of
// information
/* second veryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongComment with plenty of
 * information */

false:
// veryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongComment with plenty of information
/* second veryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongComment with plenty of information */
```

#### SortIncludes:    true
* 给 `#include` 排序.

#### SpaceAfterCStyleCast: false
* C风格的类型转换之后添加空格.

```c++
// false:
(int)i;

// true:
(int) i;
```

#### SpaceBeforeAssignmentOperators: true
* 赋值运算符之前留一个空格.

```c++
// true:
a = 3;

// false:
a= 3;
```

#### SpaceBeforeParens: ControlStatements
* 定义什么时候小括号前留一个空格:
    * Never
    * Always
    * ControlStatements: 只在控制关键字(for/if/while...)后
    * NonEmptyParentheses: 只要括号内有东西就在小括号前面留一个空格, 包括函数调用

#### SpaceInEmptyParentheses: false
* 空小括号内留一个空格.

```c++
// false:
void f() {}

// true:
void f( ) {}
```

#### SpacesBeforeTrailingComments: 2
* 尾置注释前面留的空格数.

#### SpacesInAngles:  false
* 尖括号内侧留空格.

```c++
// false:
static_cast<int>(arg);

// true:
static_cast< int >(arg);
```

#### SpacesInContainerLiterals: true
* 容器字面值内留空格. (ObjC/JavaScript)

#### SpacesInCStyleCastParentheses: false
* C类型强制类型转换时, 括号内留空格.

```c++
// false:
(int)i;

// true:
( int )i;
```

#### SpacesInParentheses: false
* 小括号内侧留空格.

```c++
// false:
t f(Deleted &) & = delete;

// true:
t f( Deleted & ) & = delete;
```

#### SpacesInSquareBrackets: false
* 在方括号内添加空格，lamda表达式和未指明大小的数组的声明不受影响.

```c++
// false:
int a[5];
std::unique_ptr<int[]> foo() {}

// true:
int a[ 5 ];
std::unique_ptr<int[]> foo() {}
```

#### Standard:        Auto
* C++标准:
    * Cpp03: `vector<set<int> > x;`
    * Cpp11: `vector<set<int>> x;`
    * Auto: 自动检测
* ***新版本使用 c++03, c++11, c++14, c++17, c++20, Latest, Auto.***

#### TabWidth:        8
* tab宽度

#### UseTab:          Never
* 使用tab字符:
    * Never
    * ForIndentation: 只在缩进时使用
    * ForContinuationAndIndentation: 只在缩进和换行时使用
    * Always

