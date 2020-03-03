# VSCode C++ 开发环境搭建

Tags : VSCode C++

---

## 安装

### Ubuntu系统

1. 在 https://code.visualstudio.com/ 官网下载对应的 .deb 安装包.
2. 安装 .deb 包: `sudo dpkg -i code_*.deb`

---

## 运行

### Ubuntu系统

```shell
code
```

### 重要快捷键

* `Ctrl` + `Shift` + `p` : 打开**命令输入框**. 命令输入框里可以输入各种 VSCode 控制指令.

---

## 安装插件

### 在线安装方式
1. 点击窗口左侧 `Extension` 图标, 会显示插件工具栏.
2. 在搜索框中搜索想要安装的插件, 找到后点击安装即可.

### 离线安装方式
1. 下载所需插件的离线安装包 `*.vsix` 文件.
2. 点击窗口左侧 `Extension` 图标, 会显示插件工具栏.
3. 在插件工具栏右上角的 `More Actions` 菜单里面选择 `Install from VSIX...`.

### 更改插件配置
1. 通过 File > Preferences > Settings 打开配置页.
2. 在 `Extensions` 目录下选择插件, 在右侧更改对应配置选项.

> **注意**: 在 `Ctrl` + `Shift` + `p` 打开的命令输入框里输入 `settings`, 会有一项 `Open Settings(JSON)`, 点击可以直接打开配置文件 `settings.json`. UI形式的配置选项和该配置文件是等效的, 只有改动项才会显示在这个文件中. 后面配置 Vim keymap 时会直接在这个文件里配置.

---

## 推荐插件

### 1. C/C++

该插件由微软官方开发, 提供C/C++开发所需的众多功能, 包括 IntelliSense, debugging, code browsing 等, 并可使用内置的 clang-format 进行代码格式化. 使用 `Ctrl`+`Shift`+`i` 组合键格式化代码.

**配置**:

* C/C++默认使用Google风格: `Clang_format_fallback Style` 设置成 `Google`.

### 2. Vim

Vim模拟器.

**配置**:

* 自己根据需要配置. 下面是我的settgins.json里面Vim相关的配置.
```json
    "vim.highlightedyank.enable": true,
    "vim.hlsearch": true,
    "vim.surround": false,
    "vim.useSystemClipboard": true,
    "vim.visualstar": true,
    "vim.leader": ",",
    "vim.handleKeys": {
        "<C-a>" : false,
        "<C-c>" : false,
    },
    "vim.insertModeKeyBindings": [
        {
            "before": ["<C-h>"],
            "after": ["<left>"]
        },
        {
            "before": ["<C-l>"],
            "after": ["<right>"]
        },
        {
            "before": ["<C-d>"],
            "after": ["<Esc>","A",";","<Esc>"]
        }
    ],
    "vim.normalModeKeyBindings": [
        {
            "before": ["<C-d>"],
            "after": ["A",";","<Esc>"]
        },
        {
            "before": ["<leader>","c"],
            "after": ["m","b","'","a","y","'","b"]
        },
        {
            "before": ["<leader>","v"],
            "after": ["m","b","'","a","d","'","b"]
        },
        {
            "before": ["<bs>"],
            "after": ["i","<bs>","<Esc>","l"]
        },
        {
            "before": ["<leader>", "w"],
            "after": ["y","i","w"]
        },
        {
            "before": ["<leader>", "<leader>"],
            "after": ["w","b","P","l","c","w","<Esc>","y","i","w"]
        }
    ],
```

### 3. Project Manager

VSCode默认只能同时打开一个项目, Project Manager可以记录多个项目, 方便项目切换.

不需要配置.


### 4. Settings Sync

同步配置信息到Github. 包括 配置文件, 快捷键, 启动文件, Snippets目录, 插件, workspace目录.

* 上传: `Shift` + `Alt` + `u`
* 下载: `Shift` + `Alt` + `d`

**配置**:

* 第一次配置

1. 首先要有 github 账户, 没有的话注册一个.
2. 安装好 Settings Sync 后会自动弹出一个 `Welcome to Settings Sync` 页面. 在该页面点击 `LOGIN WITH GITHUB` 登录github进行账户授权.
3. 在 Github 的 Settings > Developer settings > Personal access tokens 下创建新的token. 权限只需勾选一个 `gist` . 将生成的 token id 记录下来.
4. 在 `Welcome to Settings Sync` 页面点击 `EDIT CONFIGURATION`, 进入配置页面. 将 token id 填入 `Access Token` 输入框.
5. 按 `Shift` + `Alt` + `u` 上传配置信息. 第一次上传会生成一个 gist id, 记录该id.
6. 将gist id填入 `EDIT CONFIGURATION` 页面的 `Gist` 或者写入 `settings.json` 的 `sync.gist` 值, 再上传一次.  将来在其它机器上配置时使用这个 gist id 即可. (这个gist id也可以在github上查, 打开该gist, URL里最后那一串就是.)
> **注意** 最下方状态栏里会显示上传状态. 如果上传成功, `OUTPUT` 窗口会输出信息, 否则可能是由于网络问题上传失败. 搞个 VPN 吧.
>
> * 可以启用 `Auto Download` 和 `Auto Upload` 自动上传下载配置.

* 其它机器上配置

1. `Ctrl` + `Shift` + `p` 打开命令框, 在命令框中输入 `sync`, 选择 `Sync: Advanced Options`, 然后选择 `Sync: Open Settings`.
2. 在打开的页面里登录github进行账户授权.
3. 在 `EDIT CONFIGURATION` 页面填入 gist id 和 token id 即可.

---

## 卸载

### Ubuntu

```shell
# 删除软件
sudo dpkg --purge code
# 删除配置(可选)
sudo rm -rf ~/.config/Code
# 删除插件(可选)
sudo rm -rf ~/.vscode
```