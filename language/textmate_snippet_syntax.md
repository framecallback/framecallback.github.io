# TextMate Snippet语法

Tags : TextMate Snippet

---

## 参考

* 官方文档: <https://macromates.com/manual/en/snippets>
* TextMate正则表达式: <https://macromates.com/manual/en/regular_expressions>

---

## 简介

* Snippets即代码片段. 可以通过几个字母的缩写即可输入大段代码, 极大减小工作量.
* 包括:
    1. 插入时运行的代码
    2. Variable(变量)
    3. Placeholder(占位符)
    4. 对输入到占位符中的数据做变换

---

## 语法

### Plain Text(一般文字)

* "$" 和 "\`" 是特殊字符, 想要显示需要转义 `\$`,

### Variable(变量)

* 可通过 `$VAR` 的方式使用变量, 支持所有的常规动态变量. 最常用变量的可能是 `TM_SELECTED_TEXT`, 代表当前所选的字符串.
* 变量可以赋默认值, 当值为空时使用.
    * 方式为 `${VAR:DEFAULT_VALUE}`, 例如 `${TM_SELECTED_TEXT: "no text selected"}`.
    * 默认值可以包含变量或shell命令, 如果默认值里含有 `}` 字符, 需要转义.
* 变量支持 regular expression replacements(正则表达式替换), 即使用正则表达式替换变量的值.
    * 格式为 `${VAR/REGEXP/FORMAT/OPTIONS}`, 例如将所选字段中的每一个非空行前增加一个 `•`, 可使用 `${TM_SELECTED_TEXT/^.+$/• $0/g}`.

### 插入shell命令

* 插入Snippets时会自动执行使用重音符 ` 括起来的shell命令, 并将结果填入命令所在处. 例如:

    ```html
    <a href="`
        if [[ $(pbpaste|wc -l) -eq 0 ]]
            then pbpaste
            else echo http://example.com/
        fi
    `">$TM_SELECTED_TEXT</a>
    ```

* shell命令中如果有重音符, 需要转义.

### Tab Stops

* 默认情况下, 插入符停在snippet的最后一个字符后面. `$0` 可以用来控制插入符最后停放的位置.
* 当需要在不同的位置输入值时, 可用`$1`-`$n`来控制插入符的位置, 刚开头在`$1`处, 按照从1到n的顺序, 通过`Tab`键跳转.

### Placeholders(占位符)

* Tab Stops也可以有默认值. 语法与变量相同, `{TAB_STOP:DEFAULT_VALUE}`.
* 默认值可包含: Text, shell命令, 其它占位符.

    ```text
    <div${1: id="${2:some_id}"}>
        $0
    </div>
    ```

### Mirrors(镜像)

* 多个地方使用同一个值时, 可以用相同的ID. 如

    ```text
    namespace ${1:avs} {

    $2

    }  // $1
    ```

### Transformations(变换)

* 有时希望镜像的文字需要稍微有些不同, 可通过正则表达式替换: `${TAB_STOP/REGEXP/FORMAT/OPTIONS}`.
* 条件替换: `FORMAT` 部分可以使用 条件替换:

    ```text
    - (${1:void})${2:methodName}
    {${1/void$|(.+)/(?1:\n\treturn nil;)/}
    }
    ```

* 条件替换语法:
    * Capture: 正则表达式匹配后, 通过 `$n` 访问 capture register id 为 `n` 的寄存器中的值. `$0` 表示entire match.
    * `(?n:INSERTION)`: 表示 `$n` 匹配时则填入 `INSERTION` 的内容, 否则不填入内容. 不需要使用`$`前缀.
    * `(?n:INSERTION:OTHERWISE)`: 表示 `$n` 匹配时则填入 `INSERTION` 的内容, 否则填入 `OTHERWISE` 的内容. 不需要使用`$`前缀.
