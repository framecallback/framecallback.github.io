# VSCode Snippet 手册

Tags : VSCode Snippet

---

## 参考

* 官方文档: <https://code.visualstudio.com/docs/editor/userdefinedsnippets>

---

## 简介

* Snippets即代码片段. 可以通过几个字母的缩写即可输入大段代码, 极大减小工作量.
* Snippets文件格式为JSON, 支持C风格的注释, 不限snippet数量.
* Snippets支持大部分[TextMate Snippet语法](https://macromates.com/manual/en/snippets), 除了 `interpolated shell code` 和 `\u`功能.

### Snippet 作用域

VSCode Snippet 作用域分两类, **language** 和 **project**.

* language:
    * language snippet file:
        * single language: "c.json", "javascript.json", ...
        * multiple language: 同global snippet file. 只是每个snippet有个`scope`域, 填入所支持的多种语言, 没有`scope`域表示对所有语言生效.
    * global snippet file: 存放在用户全局配置目录下, 以 `.code-snippets` 结尾的文件.
* project: 放在项目目录下的 `.vscode` 目录里面的 `.code-snippets` 结尾的文件.

---

## 设置

* **创建Snippets**: File > Preferences > User Snippets
    * 或者选择对应语言的snippets
    * 或者选择 `New Global Snippets file` 为所有语言共享的snippets.
    * 或者选择 `New Snippets file for '*'` 为特定的project创建snippets.

---

## Syntax

```json
    "SNIPPET_NAME": {
        "scope": "LANGUAGE1,LANGUAGE2,...",  // 作用域. 可选
        "prefix": "xxx",  // 提示字符串. 输入该字符串, 可扩展为"body"内容
        "body": [  // 扩展后的内容
            ...
        ],
        "description": "xxx"  // 描述信息
    }
```

"body"内部可以通过特殊结构和语法来控制所插入的字符串内容以及光标位置.

### Tabstops

* `$1`-`$n` 控制光标位置, 通过 `Tab` 键跳转.

### Placeholders

* Placeholders是Tabstop带上默认值. `${1:foo}`.
* 可以嵌套: `${1:another ${2:placeholder}}`.

### Choice

* 可以给出选择列表, 用逗号隔开. `${1|one,two,three|}`.

### Variables

* 通过 `$VAR` 或者 `${VAR:DEFAULT_VALUE}` 的方式插入变量的值.
    * 变量为空时插入空字符串或 `DEFAULT_VALUE`.
    * 变量未定义时使用变量名 `VAR`, 并且该变量转变为Placeholder.
* 可用变量列表:
    * `TM_SELECTED_TEXT` The currently selected text or the empty string
    * `TM_CURRENT_LINE` The contents of the current line
    * `TM_CURRENT_WORD` The contents of the word under cursor or the empty string
    * `TM_LINE_INDEX` The zero-index based line number
    * `TM_LINE_NUMBER` The one-index based line number
    * `TM_FILENAME` The filename of the current document
    * `TM_FILENAME_BASE` The filename of the current document without its extensions
    * `TM_DIRECTORY` The directory of the current document
    * `TM_FILEPATH` The full file path of the current document
    * `CLIPBOARD` The contents of your clipboard
    * `WORKSPACE_NAME` The name of the opened workspace or folder
* 日期时间:
    * `CURRENT_YEAR` The current year
    * `CURRENT_YEAR_SHORT` The current year's last two digits
    * `CURRENT_MONTH` The month as two digits (example '02')
    * `CURRENT_MONTH_NAME` The full name of the month (example 'July')
    * `CURRENT_MONTH_NAME_SHORT` The short name of the month (example 'Jul')
    * `CURRENT_DATE` The day of the month
    * `CURRENT_DAY_NAME` The name of day (example 'Monday')
    * `CURRENT_DAY_NAME_SHORT` The short name of the day (example 'Mon')
    * `CURRENT_HOUR` The current hour in 24-hour clock format
    * `CURRENT_MINUTE` The current minute
    * `CURRENT_SECOND` The current second
    * `CURRENT_SECONDS_UNIX` The number of seconds since the Unix epoch
* 语言相关的注释:
    * `BLOCK_COMMENT_START` Example output: in PHP `/*` or in HTML `<!--`
    * `BLOCK_COMMENT_END` Example output: in PHP `*/` or in HTML `-->`
    * `LINE_COMMENT` Example output: in PHP `//`

### Variable Transforms

* 格式: `${VAR/REGEXP/FORMAT/OPTIONS}`
* 示例:
    | Example                             | Output                  | Explanation                        |
    | :---------------------------------- | :---------------------- | :--------------------------------- |
    | `${TM_FILENAME/[\\.]/_/}`           | example-123_456-TEST.js | Replace the first `.` with `_`     |
    | `${TM_FILENAME/[\\.-]/_/g}`         | example_123_456_TEST_js | Replace each `.` or `-` with `_`   |
    | `${TM_FILENAME/(.*)/${1:/upcase}/}` | EXAMPLE-123.456-TEST.JS | Change to all uppercase            |
    | `${TM_FILENAME/[^0-9^a-z]//gi}`     | example123456TESTjs     | Remove non-alphanumeric characters |

### Grammar

```text
any         ::= tabstop | placeholder | choice | variable | text
tabstop     ::= '$' int
                | '${' int '}'
                | '${' int  transform '}'
placeholder ::= '${' int ':' any '}'
choice      ::= '${' int '|' text (',' text)* '|}'
variable    ::= '$' var | '${' var '}'
                | '${' var ':' any '}'
                | '${' var transform '}'
transform   ::= '/' regex '/' (format | text)+ '/' options
format      ::= '$' int | '${' int '}'
                | '${' int ':' '/upcase' | '/downcase' | '/capitalize' '}'
                | '${' int ':+' if '}'
                | '${' int ':?' if ':' else '}'
                | '${' int ':-' else '}' | '${' int ':' else '}'
regex       ::= JavaScript Regular Expression value (ctor-string)
options     ::= JavaScript Regular Expression option (ctor-options)
var         ::= [_a-zA-Z] [_a-zA-Z0-9]*
int         ::= [0-9]+
text        ::= .*
```
