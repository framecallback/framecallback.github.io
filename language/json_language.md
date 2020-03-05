# JSON Language

Tags : JSON

---

## 参考

* 官方文档: <https://www.json.org/json-zh.html>
* w3school教程: <https://www.w3school.com.cn/json/index.asp>

---

## 简介

* JSON(JavaScript Object Notation) 是一种轻量级的文本数据交换格式.
* 对比 XML:
    * JSON 比 XML 更小, 更快, 更易解析.
    * JSON 有数组, XML 没有.
    * JSON 没有保留关键字.
* JSON 文本格式在语法上与创建 JavaScript 对象的代码相同, 无需解析器, JavaScript 程序能够使用内建的 `eval()` 函数, 用 JSON 数据来生成原生的 JavaScript 对象.
* 文件类型为 `.json`.

---

## 语法

* JSON 描述两种结构: **Object** 和 **Array**.
    * **Object** 是保存 **Name-Value Pair** (键值对) 的一个无序Map. 格式为: `{Name:Value, Name:Value, ...}`
        * **Value** 可以是6种类型之一:
            * 数字(整数/浮点数): `\-?(0|[1-9]\d*)(\.\d+)?([Ee][\+\-]?\d+)?`
                * 示例: `3`, `-0.304`, `-123.4e-8`
            * 字符串: 使用双引号 `""` 包裹, 除了 `"` 和 `\`.
                * 可以转义的字符: `"`, `\`, `/`, `b`, `f`, `n`, `r`, `t`, `uXXXX`.
            * Array
            * Object
            * 布尔值: `true` 或 `false`
            * 空值: `null`
        * **Name** 必须是字符串.
    * **Array** 是保存 **Value** 的一个有序数组. 格式为 `[Value, Value, ...]`.

---

## library

### [C++] nlohmann/json

* 项目地址: <https://github.com/nlohmann/json>
* 特点:
    * 单个文件, 只需将 `json.hpp` 文件放入工程即可.
    * 接口友善, 易于使用.
    * 测试充分.
    * 基于C++11.
    * Memory和Speed性能不极致, 一般项目无需关心这些.
