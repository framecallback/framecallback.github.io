# Markdown手册

Tags ：Markdown

---

## 简介

* Markdown 是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档。
* Markdown 编写的文档可以导出 HTML 、Word、图像、PDF、Epub 等多种格式的文档。
* Markdown 编写的文档后缀为 .md, .markdown。
* Markdown 能被使用来撰写电子书，如：Gitbook。当前许多网站都广泛使用 Markdown 来撰写帮助文档或是用于论坛上发表消息。例如：GitHub、简书、reddit、SourceForge等。

## 工具

* 编辑器: Typora, 编辑后直接渲染出效果。支持导出HTML、PDF、Word、图片等多种类型文件。
* 在线编辑器: Cmd Markdown, https://www.zybuluo.com
* HTML字符在线编码转换: https://tool.oschina.net/encode

## 语法

### 标题

方式1. 使用`#`格式可表示6级标题(推荐)
```
# 一级标题(#后面一定要有一个空格)
## 二级标题(#后面一定要有一个空格)
### 三级标题(#后面一定要有一个空格)
#### 四级标题(#后面一定要有一个空格)
##### 五级标题(#后面一定要有一个空格)
###### 六级标题(#后面一定要有一个空格)
```

方式2. `=====`和`-----`格式可表示2级标题
```markdown
一级标题
===========

二级标题
-----------
```

### 段落

1. 使用空白行(推荐)
2. 行末使用多个空格(Typora渲染不支持)

### 字体

* 斜体`*xxx*`, `_xxx_`。`*xxx*`显示为*xxx*。
* 粗体`**xxx**`, `__xxx__`。`**xxx**`显示为**xxx**。
* 斜粗体`***xxx***`, `___xxx___`。`***xxx***`显示为***xxx***。

### 分隔线

一行中用三个以上的星号`*`、减号`-`、底线`_`来建立一个分隔线，行内不能有其他东西。可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：
```markdown
***
---
___
* * *
_  _    _
```

### 删除线

    ~~xxx~~
显示为~~xxx~~

### 下划线

`<u>xxx</u>`显示为 <u>xxx</u> 。（Cmd Markdown显示有问题)

### 脚注

> 好像各个渲染器得到的都不一致，慎用。

```
a[^xxx]

[^xxx]: xxx的注释字段
```
显示为a[^xxx]

[^xxx]: xxx的注释字段

### 列表

#### 无序列表(*, +, -)

 * 第一项
 * 第二项
 * 第三项

#### 有序列表(N. xxx)

 1. 第一项
 2. 第二项
 3. 第三项

#### 子列表(前面加4个空格)

 1. 第一项
     1. 第一.一项
     2. 第一.二项
 2. 第二项

### 区块引用

* 区块引用是在段落开头使用`>`符号 ，然后后面紧跟一个空格符号。
* 区块是可以嵌套的。
* 区块中可以使用列表， 列表中也可以使用区块, 列表中使用区块时要注意区块前的子列表缩进。

```markdown
> NOTE:
> > 1. dog
> > 
> > 2. cat
>
> > both big
> 
> run away
```

> NOTE:
> > 1. dog
> > 
> > 2. cat
>
> > both big
> 
> run away

### 代码

#### 行内代码片段

    哈哈`foo(x)`嘿
显示: 哈哈`foo(x)`嘿

#### 代码段落

1. 指定语言(\`\`\`包裹代码段)

        ```c++
        int main() {
        return 0;
        }
        ```

2. 普通代码段落(四个空格缩进)
    ```
        int main() {
            return 0;
        }
    ```

### 链接

1. 普通方式: `[链接名称](链接地址)`
2. 普通方式: `(链接地址)`
3. 变量方式: `[链接名称][变量名称]`

    ```
    这个链接用 1 作为网址变量 [Google][1]
    这个链接用 runoob 作为网址变量 [Runoob][runoob]
    然后在文档的结尾为变量赋值（网址）
    
    [1]: http://www.google.com/
    [runoob]: http://www.runoob.com/</nowiki>
    ```
显示为:
这个链接用 1 作为网址变量 [Google][1]
这个链接用 runoob 作为网址变量 [Runoob][runoob]
然后在文档的结尾为变量赋值（网址）

[1]: http://www.google.com/
[runoob]: http://www.runoob.com/</nowiki>


### 图片

1. 普通: `![替代文本(可选)](图片地址 "title"(可选))`

2. 缩放(使用html img标签): `<img src="xxxxxx" alt="text" width="50%"/>`
```html
<img src="img/pikachu.jpeg" alt="pikachu" width="20%"/>
```
<img src="img/pikachu.jpeg" alt="pikachu" width="20%"/>

3. 图片居中使用html div标签

```
<div align=center>
<img src="img/pikachu.jpeg" alt="pikachu" width="20%"/>
</div>
```

<div align=center>
<img src="img/pikachu.jpeg" alt="pikachu" width="20%"/>
</div>

   

### 表格

表格使用`|`来分隔不同的单元格，使用`-`来分隔表头和其他行。
对齐方式

* `-:` 设置内容和标题栏居右对齐。
* `:-` 设置内容和标题栏居左对齐。
* `:-:` 设置内容和标题栏居中对齐。

```
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
```
显示为:

| 左对齐 | 右对齐 | 居中对齐 |
| :----- | -----: | :------: |
| 单元格 | 单元格 |  单元格  |
| 单元格 | 单元格 |  单元格  |

### 公式

使用TeX 或 LaTeX 格式的数学公式。提交后，问答和文章页会根据需要加载 Mathjax 对数学公式进行渲染。

#### 行内显示(, 非标准功能，Typora可选支持)

用单个美元符包裹`$...$`, `$f(y)=x^3$`显示为$f(y)=x^3$。

#### 单行显示

可以使用两个美元符包裹`$$...$$`。
```text
$$
 \mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
 \mathbf{i} & \mathbf{j} & \mathbf{k} \\
 \frac{\partial X}{\partial u} & \frac{\partial Y}{\partial u} & 0 \\
 \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
 \end{vmatrix}
$$
```
显示为:
$$
 \mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix}
 \mathbf{i} & \mathbf{j} & \mathbf{k} \\
 \frac{\partial X}{\partial u} & \frac{\partial Y}{\partial u} & 0 \\
 \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
 \end{vmatrix}
$$

## 高级技巧

### 支持的HTML元素

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。
目前支持的 HTML 元素有：`<kbd>` `<b>` `<i>` `<em>` `<sup>` `<sub>` `<br>`等 ，如：

    使用<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd>重启电脑

显示为: 使用<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd>重启电脑

### 转义(\\)

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：
```text
\   反斜线
`   反引号
*   星号
_   下划线
{}  花括号
[]  方括号
()  小括号
#   井字号
+   加号
-   减号
.   英文句点
!   感叹号
```

### 下标(`~xxx~`, Typora扩展)
### 上标(`^xxx^`, Typora扩展)
### 高亮(`==xxx==`, Typora扩展)

