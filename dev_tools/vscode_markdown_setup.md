# VSCode Markdown 设置

Tags : VSCode Markdown

---

## 快捷键

* `Ctrl` + `Shift` + `v` : 显示Markdown预览.

---

## Snippets设置

1. settings.json 里面添加

    ```json
        "[markdown]": {
            "editor.quickSuggestions": {
                "other": true,
                "comments": false,
                "strings": false
            },
        },
    ```

2. File > Preferences > User Snippets > markdown 里面添加自己的 Markdown Snippets.

---

## 插件

### Markdown All in One

* `Ctrl` + `Shift` + `i` : 格式化

### markdownlint

* markdown 格式规范化工具. 实时显示格式问题.
* 参数说明: <https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md>

**配置**:

```json
    "markdownlint.config": {
        "default": true,
        "MD007": { "indent": 4 },
        "MD033": { "allowed_elements": ["u", "img", "div", "kbd", "b", "i", "em", "sup", "sub", "br"] },
        "MD046": { "style": "fenced" },
    },
```
