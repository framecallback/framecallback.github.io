# Jupyter Notebook手册

Tags : Jupyter

---



## 参考

* Jupyter官网: https://jupyter.org/
* Jupyter官方文档: https://jupyter.org/documentation



## 简介

* Jupyter Notebook 是一个在浏览器中使用的交互式的笔记本，可以实现将代码、文字完美结合起来，它的受众群体大多数是一些从事数据科学领域相关（机器学习、数据分析等）的人员。
* 不仅可以运行书写的python代码，同时还支持markdown格式的文本显示。
* 在Notebooks中不仅可以运行python，它还支持R、Julia 和 JavaScript等其他40余种语言。



## 安装

推荐使用集成科学计算环境Anaconda。



### 安装Anaconda

#### Ubuntu18.04系统
在[清华镜像网站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)下载最新的Anaconda。

1. 安装
    ```shell
    bash Anaconda*.sh
    ```

2. 阅读license，输入回车`Enter`
    ```shell
    In order to continue the installation process, please review the license
    agreement.
    Please, press ENTER to continue
    >>> 
    ```

3. 同意License, 输入`yes`
    ```shell
    Do you accept the license terms? [yes|no]
    [no] >>> 
    Please answer 'yes' or 'no':'
    >>> yes
    ```
    
4. 选择安装路径，默认输入回车`Enter`
    ```shell
    Anaconda3 will now be installed into this location:
    /home/tyrael/anaconda3

      - Press ENTER to confirm the location
      - Press CTRL-C to abort the installation
      - Or specify a different location below
    
    [/home/tyrael/anaconda3] >>>
    ```
    
5. 初始化Anaconda3，输入`yes`
    ```shell
    Do you wish the installer to initialize Anaconda3
    in your /home/tyrael/.bashrc ? [yes|no]
    [no] >>> yes
    ```

6. 是否安装VS Code，输入`no`
    ```shell
    Do you wish to proceed with the installation of Microsoft VSCode? [yes|no]
    >>> no
    ```
    
7. 修改包管理镜像为国内源
    ```shell
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --set show_channel_urls yes
    ```
    

安装完Anaconda就可以直接使用Jupyter Notebook了。



## 启动

```shell
cd "jupyter work dir"
jupyter-notebook
```



通过`jupyter-notebook --help`查询启动参数。

### 子命令

子命令调用格式为: `jupyter-notebook cmd [args]`, 例如子命令帮助信息`jupyter-notebook cmd -h`。

| 子命令   | 功能                              |
| -------- | --------------------------------- |
| list     | 列举所有当前运行的notebook server |
| stop     | 根据给定端口号停止相应的server    |
| password | 给server设置密码                  |

### 常用参数

| 参数名                   | 功能                                                         |
| ------------------------ | ------------------------------------------------------------ |
| --help                   | 显示帮助信息(可列举全部可用参数)                             |
| --generate-config        | 生成配置文件                                                 |
| --no-browser             | 启动后不弹出浏览器页面                                       |
| --no-mathjax             | 禁止MathJax                                                  |
| --log-level=<Enum>       | (0, 10, 20, 30, 40, 50, 'DEBUG', 'INFO', 'WARN', 'ERROR', 'CRITICAL')，默认30 |
| --ip=<Unicode>           | 指定server监听的IP，默认'localhost'                          |
| --port=<Int>             | 指定server监听的端口，默认8888                               |
| --notebook-dir=<Unicode> | server的工作目录                                             |

示例：

    jupyter notebook                       # start the notebook
    jupyter notebook --certfile=mycert.pem # use SSL/TLS certificate
    jupyter notebook password              # enter a password to protect the server



## 配置(可选)

```
# 生成配置文件
jupyter-notebook --generate-config

# 修改配置文件
vi ~/.jupyter/jupyter_notebook_config.py
```



## 使用说明

* notebook文档是一个以.ipynb后缀结尾的JSON文件
* 通过`nbconvert`可以导出成多种格式，HTML, reStructuredText, LaTeX, PDF, and slide shows。



### 文件结构

notebook文档由多个单元格(cell)组成，cell有三种类型: code cell, markdown cell, raw cell。可以通过控件或快捷键更改cell类型。

#### code cell

内含一段代码可执行的代码。编程语言取决于所选用的kernel类型，默认的kernel(IPython)运行Python代码。

当一个code cell运行时，其代码被发送到该notebook所关联的kernel上，计算结果随后显示在notebook上并作为cell的输出。输出结果不局限于text，也支持其它格式如`matplotlib`图像，HTML表格等。IPython的Rich Output能够输出HTML,JSON,PNG,JPEG,SVG,LaTeX。

Rich Output示例: https://nbviewer.jupyter.org/github/ipython/ipython/blob/master/examples/IPython%20Kernel/Rich%20Output.ipynb

#### Markdown cell

内含一段Markdown代码。点击运行会直接渲染成相应格式。可以在此部分写文本、公式、贴图、链接等。

#### Raw Cell

Raw cell内的内容不会被notebook处理，直接作为输入。



### Basic Workflow

基本流程与IPython不同的地方在于，notebook的cell可以反复修改，知道运行得到理想的结果。可以将一段长程序分成几个多个程序片段，在前面cell都正确运行后调试下一个cell，可以节省大量时间。