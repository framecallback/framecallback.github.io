# VSCode Markdown 设置

Tags : VSCode Markdown

---

## 快捷键

* `Ctrl` + `Shift` + `v` : 显示Markdown预览.

---

## Snippets设置

1. settings.json 里面添加
```
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
