# docsify手册


Tags ：docsify

---



## 简介

### 参考

* https://docsify.js.org/#/zh-cn/ docsify中文文档



### 安装

Ubuntu18.04下:
```shell
# 安装node
sudo apt install nodejs npm
# 升级node
sudo npm install -g n
sudo n stable 稳定版
sudo n
# 升级npm
sudo npm i -g npm
# 安装docsify-cli
sudo npm i docsify-cli -g
```



## 入门

### 初始化项目

```shell
# ./docs是github推荐的文档目录
docsify init ./docs
```



### 本地预览

```shell
docsify serve ./docs
```
用浏览器访问`localhost:3000`。



### 设置Loading提示

初始化时会显示 `Loading...` 内容，你可以自定义提示信息。在index.html中配置:
```html
<div id="app">Loading...</div>
```



### 多页文档

* 用`[显示信息](绝对路径或相对路径)`方式链接，绝对路径的根目录为./docs。
* .md文件后缀名可以省略，README.md可以省略。

假设目录结构为
```text
-| docs/
  -| README.md
  -| guide.md
  -| zh-cn/
    -| README.md
    -| guide.md
```
则
```text
guide        => docs/guide.md
/guide       => docs/guide.md
zh-cn/       => docs/zh-cn/README.md
zh-cn/guide  => docs/zh-cn/guide.md
```



### 定制侧边栏

默认情况下侧边栏会通过 Markdown 文件自动生成，使用当前页面的标题目录。不方便。最好定制自己的侧边栏。

1. index.html里配置`loadSidebar`选项。

   ```html
   <script>
     window.$docsify = {
       loadSidebar: true
     }
   </script>
   <script src="//unpkg.com/docsify"></script>
   ```

2. 在文档根目录创建 `.nojekyll` 命名的空文件，阻止 GitHub Pages 忽略命名是下划线开头的文件。

3. 创建 `_sidebar.md` 文件。`_sidebar.md` 的加载逻辑是从每层目录下获取文件，如果当前目录不存在该文件则回退到上一级目录。也可以配置 `alias` 避免不必要的回退过程。

   ```html
   <script>
     window.$docsify = {
       loadSidebar: true,
       alias: {
         '/.*/_sidebar.md': '/_sidebar.md'
       }
     }
   </script>
   ```



### 显示目录

自定义侧边栏同时也可以开启目录功能。index.html中设置 `subMaxLevel` ，配置显示的目录深度。

```html
<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2
  }
</script>
<script src="//unpkg.com/docsify"></script>
```



### 忽略指定标题

当设置了 `subMaxLevel` 时，默认情况下每个标题都会自动添加到目录中。如果你想忽略特定的标题，可以给它添加 `{docsify-ignore}` 。

```markdown
# Getting Started

## HeaderNeedToBeIgnored {docsify-ignore}
```

要忽略特定页面上的所有标题，你可以在页面的第一个标题上使用 `{docsify-ignore-all}` 。
```markdown
# Getting Started {docsify-ignore-all}

## HeaderNeedToBeIgnored
```



### 定制导航栏

1. index.html里配置`loadNavbar: true`，默认加载的文件为 `_navbar.md`。

   ```html
   <script>
     window.$docsify = {
       loadNavbar: true
     }
   </script>
   <script src="//unpkg.com/docsify"></script>
   ```

2. 创建`_navbar.md`。`_navbar.md` 加载逻辑和 `_sidebar.md` 文件一致，从每层目录下获取。

3. 如果导航内容过多，可以写成嵌套的列表，会被渲染成下拉列表的形式。

   例如:

   ```markdown
   * 基础
     * [快速开始](zh-cn/quickstart.md)
     * [多页文档](zh-cn/more-pages.md)
     * [定制导航栏](zh-cn/custom-navbar.md)
     * [封面](zh-cn/cover.md)
   
   * 配置
     * [配置项](zh-cn/configuration.md)
     * [主题](zh-cn/themes.md)
     * [使用插件](zh-cn/plugins.md)
     * [Markdown 配置](zh-cn/markdown.md)
     * [代码高亮](zh-cn/language-highlight.md)
   ```

   

### 封面

1. 通过index.html设置 `coverpage` 参数，可以开启渲染封面的功能。默认加载`_coverpage.md`。

    ```html
    <script>
      window.$docsify = {
        coverpage: true
      }
    </script>
    <script src="//unpkg.com/docsify"></script>
    ```

2. 创建`_coverpage.md`。一份文档只会在根目录下加载封面，其他页面或者二级目录下都不会加载。

3. 默认背景是随机生成的渐变色。可以在文档末尾用添加图片的 Markdown 语法设置背景。
   ```
   # docsify
   [GitHub](https://github.com/docsifyjs/docsify/)
   [Get Started](#quick-start)
   
   <!-- 背景图片 -->
   ![](_media/bg.png)
   
   <!-- 背景色 -->
   ![color](#f0f0f0)
   ```

4. 如果你的文档网站是多语言的，或许你需要设置多个封面。例如你的文档目录结构如下：

   ```text
   .
   └── docs
       ├── README.md
       ├── guide.md
       ├── _coverpage.md
       └── zh-cn
           ├── README.md
           └── guide.md
           └── _coverpage.md
   ```

   那么你可以这么配置

   ```html
   window.$docsify = {
     coverpage: ['/', '/zh-cn/']
   };
   ```

   或者具体指名文件名

   ```html
   window.$docsify = {
     coverpage: {
       '/': 'cover.md',
       '/zh-cn/': 'cover.md'
     }
   };
   ```


## 定制化

### 配置项

配置在index.html的 `window.$docsify` 里。

#### el

- 类型：`String`
- 默认值：`#app`

docsify 初始化的挂载元素，可以是一个 CSS 选择器，默认为 `#app` 如果不存在就直接绑定在 `body` 上。

```js
window.$docsify = {
  el: '#app'
};
```

#### repo

- 类型：`String`
- 默认值: `null`

配置仓库地址或者 `username/repo` 的字符串，会在页面右上角渲染一个 [GitHub Corner](http://tholman.com/github-corners/) 挂件。

```
window.$docsify = {
  repo: 'docsifyjs/docsify',
  // or
  repo: 'https://github.com/docsifyjs/docsify/'
};
```

#### maxLevel

- 类型：`Number`
- 默认值: `6`

默认情况下会抓取文档中所有标题渲染成目录，可配置最大支持渲染的标题层级。

```
window.$docsify = {
  maxLevel: 4
};
```

#### loadNavbar

- 类型：`Boolean|String`
- 默认值: `false`

加载自定义导航栏，参考[定制导航栏](#定制导航栏) 了解用法。设置为 `true` 后会加载 `_navbar.md` 文件，也可以自定义加载的文件名。

```
window.$docsify = {
  // 加载 _navbar.md
  loadNavbar: true,

  // 加载 nav.md
  loadNavbar: 'nav.md'
};
```

#### loadSidebar

- 类型：`Boolean|String`
- 默认值: `false`

加载自定义侧边栏，参考[多页文档](#多页文档)。设置为 `true` 后会加载 `_sidebar.md` 文件，也可以自定义加载的文件名。

```
window.$docsify = {
  // 加载 _sidebar.md
  loadSidebar: true,

  // 加载 summary.md
  loadSidebar: 'summary.md'
};
```

#### subMaxLevel

- 类型：`Number`
- 默认值: `0`

自定义侧边栏后默认不会再生成目录，你也可以通过设置生成目录的最大层级开启这个功能。

```
window.$docsify = {
  subMaxLevel: 2
};
```

#### auto2top

- 类型：`Boolean`
- 默认值: `false`

切换页面后是否自动跳转到页面顶部。

```
window.$docsify = {
  auto2top: true
};
```

#### homepage

- 类型：`String`
- 默认值: `README.md`

设置首页文件加载路径。适合不想将 `README.md` 作为入口文件渲染，或者是文档存放在其他位置的情况使用。

```
window.$docsify = {
  // 入口文件改为 /home.md
  homepage: 'home.md',

  // 文档和仓库根目录下的 README.md 内容一致
  homepage:
    'https://raw.githubusercontent.com/docsifyjs/docsify/master/README.md'
};
```

#### basePath

- 类型：`String`

文档加载的根路径，可以是二级路径或者是其他域名的路径。

```
window.$docsify = {
  basePath: '/path/',

  // 直接渲染其他域名的文档
  basePath: 'https://docsify.js.org/',

  // 甚至直接渲染其他仓库 readme
  basePath:
    'https://raw.githubusercontent.com/ryanmcdermott/clean-code-javascript/master/'
};
```

#### coverpage

- 类型：`Boolean|String`
- 默认值: `false`

启用[封面页](#封面)。开启后是加载 `_coverpage.md` 文件，也可以自定义文件名。

```
window.$docsify = {
  coverpage: true,

  // 自定义文件名
  coverpage: 'cover.md',

  // mutiple covers
  coverpage: ['/', '/zh-cn/'],

  // mutiple covers and custom file name
  coverpage: {
    '/': 'cover.md',
    '/zh-cn/': 'cover.md'
  }
};
```

#### logo

- 类型: `String`

在侧边栏中出现的网站图标，你可以使用`CSS`来更改大小

```
window.$docsify = {
  logo: '/_media/icon.svg'
};
```

#### name

- 类型：`String`

文档标题，会显示在侧边栏顶部。

```
window.$docsify = {
  name: 'docsify'
};
```

#### nameLink

- 类型：`String`
- 默认值：`window.location.pathname`

点击文档标题后跳转的链接地址。

```
window.$docsify = {
  nameLink: '/',

  // 按照路由切换
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/': '/'
  }
};
```

#### markdown

- 类型: `Object|Function`

参考 [Markdown 配置](#Markdown配置)。

```
window.$docsify = {
  // object
  markdown: {
    smartypants: true,
    renderer: {
      link: function() {
        // ...
      }
    }
  },

  // function
  markdown: function(marked, renderer) {
    // ...
    return marked;
  }
};
```

#### themeColor

- 类型：`String`

替换主题色。利用 [CSS3 支持变量](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables)的特性，对于老的浏览器有 polyfill 处理。

```
window.$docsify = {
  themeColor: '#3F51B5'
};
```

#### alias

- 类型：`Object`

定义路由别名，可以更自由的定义路由规则。 支持正则。

```
window.$docsify = {
  alias: {
    '/foo/(+*)': '/bar/$1', // supports regexp
    '/zh-cn/changelog': '/changelog',
    '/changelog':
      'https://raw.githubusercontent.com/docsifyjs/docsify/master/CHANGELOG',
    '/.*/_sidebar.md': '/_sidebar.md' // See #301
  }
};
```

#### autoHeader

- 类型：`Boolean`

同时设置 `loadSidebar` 和 `autoHeader` 后，可以根据 `_sidebar.md` 的内容自动为每个页面增加标题。

```
window.$docsify = {
  loadSidebar: true,
  autoHeader: true
};
```

#### executeScript

- 类型：`Boolean`

执行文档里的 script 标签里的脚本，只执行第一个 script。 如果 Vue 存在，则自动开启。

```
window.$docsify = {
  executeScript: true
};
## This is test

<script>
  console.log(2333)
</script>
```

注意如果执行的是一个外链脚本，比如 jsfiddle 的内嵌 demo，请确保引入 [external-script](https://github.com/docsifyjs/docs-zh/blob/master/plugins.md?id=外链脚本-external-script) 插件。

#### noEmoji

- 类型: `Boolean`

禁用 emoji 解析。

```
window.$docsify = {
  noEmoji: true
};
```

#### mergeNavbar

- 类型: `Boolean`

小屏设备下合并导航栏到侧边栏。

```
window.$docsify = {
  mergeNavbar: true
};
```

#### formatUpdated

- 类型: `String|Function`

我们可以通过 **{docsify-updated}** 变量显示文档更新日期. 并且通过 `formatUpdated`配置日期格式。参考 https://github.com/lukeed/tinydate#patterns

```
window.$docsify = {
  formatUpdated: '{MM}/{DD} {HH}:{mm}',

  formatUpdated: function(time) {
    // ...

    return time;
  }
};
```

#### externalLinkTarget

- 类型: `String`
- 默认: `_blank`

当前默认为 _blank, 配置一下就可以：

```
window.$docsify = {
  externalLinkTarget: '_self' // default: '_blank'
};
```

#### routerMode

- 类型: `String`
- 默认: `hash`

```
window.$docsify = {
  routerMode: 'history' // default: 'hash'
};
```

#### noCompileLinks

- 类型: `Array`

有时我们不希望 docsify 处理我们的链接。 参考 [#203](https://github.com/docsifyjs/docsify/issues/203)

```
window.$docsify = {
  noCompileLinks: ['/foo', '/bar/.*']
};
```

#### requestHeaders

- 类型: `Object`

设置请求资源的请求头。

```
window.$docsify = {
  requestHeaders: {
    'x-token': 'xxx'
  }
};
```

#### ext

- 类型: `String`

资源的文件扩展名。

```
window.$docsify = {
  ext: '.md'
};
```

#### fallbackLanguages

- 类型: `Array`

一个语言列表。在浏览这个列表中的语言的翻译文档时都会在请求到一个对应语言的翻译文档，不存在时显示默认语言的同名文档

Example:

- 尝试访问`/de/overview`，如果存在则显示
- 如果不存在则尝试`/overview`（取决于默认语言），如果存在即显示
- 如果也不存在，显示404页面

```
window.$docsify = {
  fallbackLanguages: ['fr', 'de']
};
```

#### notFoundPage

- 类型: `Boolean` | `String` | `Object`

在找不到指定页面时加载`_404.md`:

```
window.$docsify = {
  notFoundPage: true
};
```

加载自定义404页面:

```
window.$docsify = {
  notFoundPage: 'my404.md'
};
```

加载正确的本地化过的404页面:

```
window.$docsify = {
  notFoundPage: {
    '/': '_404.md',
    '/de': 'de/_404.md'
  }
};
```

> 注意: 配置过`fallbackLanguages`这个选项的页面与这个选项`notFoundPage`冲突。



### 主题

在index.html里更改主题。目前支持的主题:

```html
<link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/buble.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/dark.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/pure.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/dolphin.css">
```

CSS 的压缩文件位于 `/lib/themes/`

```html
<link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/vue.css">
<link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/buble.css">
<link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/dark.css">
<link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/pure.css">
<link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/dolphin.css">
```

#### 其它主题

* [docsify-themeable](https://jhildenbiddle.github.io/docsify-themeable/#/) 一个用于docsify的，简单到令人愉悦的主题系统.



### 插件

#### 全文搜索 - Search

全文搜索插件会根据当前页面上的超链接获取文档内容，在 `localStorage` 内建立文档索引。默认过期时间为一天，当然我们可以自己指定需要缓存的文件列表或者配置过期时间。

```html
<script>
  window.$docsify = {
    search: 'auto', // 默认值

    search : [
      '/',            // => /README.md
      '/guide',       // => /guide.md
      '/get-started', // => /get-started.md
      '/zh-cn/',      // => /zh-cn/README.md
    ],

    // 完整配置参数
    search: {
      maxAge: 86400000, // 过期时间，单位毫秒，默认一天
      paths: [], // or 'auto'
      placeholder: 'Type to search',

      // 支持本地化
      placeholder: {
        '/zh-cn/': '搜索',
        '/': 'Type to search'
      },

      noData: 'No Results!',

      // 支持本地化
      noData: {
        '/zh-cn/': '找不到结果',
        '/': 'No Results'
      },

      // 搜索标题的最大程级, 1 - 6
      depth: 2
    }
  }
</script>
<script src="//unpkg.com/docsify"></script>
<script src="//unpkg.com/docsify/lib/plugins/search.js"></script>
```

#### google统计 - Google Analytics

需要配置 track id 才能使用。

```html
<script>
  window.$docsify = {
    ga: 'UA-XXXXX-Y'
  }
</script>
<script src="//unpkg.com/docsify"></script>
<script src="//unpkg.com/docsify/lib/plugins/ga.js"></script>
```

也可以通过 `data-ga` 配置 id。

```html
<script src="//unpkg.com/docsify" data-ga="UA-XXXXX-Y"></script>
<script src="//unpkg.com/docsify/lib/plugins/ga.js"></script>
```

#### emoji

默认是提供 emoji 解析的，能将类似 `:100:` 解析成![100](https://github.githubassets.com/images/icons/emoji/100.png)。但是它不是精准的，因为没有处理非 emoji 的字符串。如果你需要正确解析 emoji 字符串，你可以引入这个插件。

```html
<script src="//unpkg.com/docsify/lib/plugins/emoji.js"></script>
```

#### 外链脚本 - External Script

如果文档里的 script 是内联脚本，可以直接执行；而如果是外链脚本（即 js 文件内容由 `src` 属性引入），则需要使用此插件。

```html
<script src="//unpkg.com/docsify/lib/plugins/external-script.js"></script>
```

#### Demo code with instant preview and jsfiddle integration

使用这个插件，示例代码可以在页面上立刻渲染，这样就可以立刻看到效果。当示例框被展开时，源码和描述会被显示出来，如果他们点击`Try in Jsfiddle`这个按钮，将会在`jsfiddle.net`中打开一个包含这些示例代码的项目，这样就可以修改源码和测试了。

docsify同时支持[Vue](https://njleonzhang.github.io/docsify-demo-box-vue/)和[React](https://njleonzhang.github.io/docsify-demo-box-react/)版本的插件。

#### 图片缩放 - Zoom image

Medium's 风格的图片缩放插件. 基于 [medium-zoom](https://github.com/francoischalifour/medium-zoom)。

```html
<script src="//unpkg.com/docsify/lib/plugins/zoom-image.js"></script>
```

忽略某张图片

```markdown
![](image.png ':no-zoom')
```

#### 在 Github 上编辑

在每一页上添加 `Edit on github` 按钮. 由第三方库提供, 查看 [document](https://github.com/njleonzhang/docsify-edit-on-github)

#### 复制到剪贴板

在所有的代码块上添加一个简单的`Click to copy` 按钮来允许用户从你的文档中轻易地复制代码。由[@jperasmus](https://github.com/jperasmus)提供。

```html
<script src="//unpkg.com/docsify-copy-code"></script>
```

从[这里](https://github.com/jperasmus/docsify-copy-code#readme)获取更多信息。

#### Disqus

Disqus评论系统支持。 https://disqus.com/

```html
<script>
  window.$docsify = {
    disqus: 'shortname'
  }
</script>
<script src="//unpkg.com/docsify/lib/plugins/disqus.min.js"></script>
```

#### Gitalk

[Gitalk](https://github.com/gitalk/gitalk)，一个现代化的，基于Preact和Github Issue的评论系统。

```html
<link rel="stylesheet" href="//unpkg.com/gitalk/dist/gitalk.css">

<script src="//unpkg.com/docsify/lib/plugins/gitalk.min.js"></script>
<script src="//unpkg.com/gitalk/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: 'Github Application Client ID',
    clientSecret: 'Github Application Client Secret',
    repo: 'Github repo',
    owner: 'Github repo owner',
    admin: ['Github repo collaborators, only these guys can initialize github issues'],
    // facebook-like distraction free mode
    distractionFreeMode: false
  })
</script>
```

#### Pagination

docsify的分页导航插件，由[@imyelo](https://github.com/imyelo)提供。

```html
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
<script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>
```

从[这里](https://github.com/imyelo/docsify-pagination#readme)获取更多信息。

#### Code Fund

帮你快速接入[Code Fund](https://codesponsor.io/)的[插件](https://github.com/njleonzhang/docsify-plugin-codefund), 由[@njleonzhang](https://github.com/njleonzhang)提供。

> Code Fund 以前叫 codesponsor

```html
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>

window.$docsify = {
  plugins: [
    DocsifyCodefund.create('51d43327-eea3-4e27-bd44-e075e67a84fb') // 把这个id改成你的codefund id
  ]
}
```



### 开发插件

docsify 提供了一套插件机制，其中提供的钩子（hook）支持处理异步逻辑，可以很方便的扩展功能。

#### 完整功能

```js
window.$docsify = {
 plugins: [
  function (hook, vm) {
    hook.init(function() {
      // 初始化时调用，只调用一次，没有参数。
    })

    hook.beforeEach(function(content) {
      // 每次开始解析 Markdown 内容时调用
      // ...
      return content
    })

    hook.afterEach(function(html, next) {
      // 解析成 html 后调用。beforeEach 和 afterEach 支持处理异步逻辑
      // ...
      // 异步处理完成后调用 next(html) 返回结果
      next(html)
    })

    hook.doneEach(function() {
      // 每次路由切换时数据全部加载完成后调用，没有参数。
      // ...
    })

    hook.mounted(function() {
      // 初始化完成后调用 ，只调用一次，没有参数。
    })

    hook.ready(function() {
      // 初始化并第一次加完成数据后调用，没有参数。
    })
  }
 ]
}
```

如果需要用 docsify 的内部方法，可以通过 `window.Docsify` 获取，通过 `vm` 获取当前实例。

#### 示例 footer:

给每个页面的末尾加上 `footer`

```js
window.$docsify = {
  plugins: [
    function (hook) {
      var footer = [
        '<hr/>',
        '<footer>',
        '<span><a href="https://github.com/QingWei-Li">cinwell</a> &copy;2017.</span>',
        '<span>Proudly published with <a href="https://github.com/docsifyjs/docsify" target="_blank">docsify</a>.</span>',
        '</footer>'
      ].join('')

      hook.afterEach(function (html) {
        return html + footer
      })
    }
  ]
}
```

#### 示例 Edit Button:

```js
window.$docsify = {
  plugins: [
    function(hook, vm) {
      hook.beforeEach(function (html) {
        var url = 'https://github.com/docsifyjs/docsify/blob/master/docs' + vm.route.file
        var editHtml = '[📝 EDIT DOCUMENT](' + url + ')\n'

        return editHtml
          + html
          + '\n----\n'
          + 'Last modified {docsify-updated} '
          + editHtml
      })
    }
  ]
}
```



### Markdown 配置

内置的 Markdown 解析器是 [marked](https://github.com/markedjs/marked)，可以修改它的配置。同时可以直接配置 `renderer`。

```js
window.$docsify = {
  markdown: {
    smartypants: true,
    renderer: {
      link: function() {
        // ...
      }
    }
  }
}
```

> 完整配置参数参考 [marked 文档](https://github.com/markedjs/marked#options-1)

当然也可以完全定制 Markdown 解析规则。

```js
window.$docsify = {
  markdown: function(marked, renderer) {
    // ...

    return marked
  }
}
```

#### 支持 mermaid

```js
// Import mermaid
//  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.css">
//  <script src="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

mermaid.initialize({ startOnLoad: false });

window.$docsify = {
  markdown: {
    renderer: {
      code: function(code, lang) {
        if (lang === "mermaid") {
          return (
            '<div class="mermaid">' + mermaid.render(lang, code) + "</div>"
          );
        }
        return this.origin.code.apply(this, arguments);
      }
    }
  }
}
```



### 代码高亮

内置的代码高亮工具是 [Prism](https://github.com/PrismJS/prism)，默认支持 CSS、JavaScript 和 HTML。如果需要高亮其语言——例如 PHP——可以手动引入代码高亮插件。

```html
<script src="//unpkg.com/docsify"></script>
<script src="//unpkg.com/prismjs/components/prism-bash.js"></script>
<script src="//unpkg.com/prismjs/components/prism-php.js"></script>
```

其他的语言高亮插件可以查看[Prims 仓库](https://github.com/PrismJS/prism/tree/gh-pages/components)。



## 部署

和 GitBook 生成的文档一样，我们可以直接把文档网站部署到 GitHub Pages 或者 VPS 上。

### GitHub Pages

GitHub Pages 支持从三个地方读取文件

- `docs/` 目录
- master 分支
- gh-pages 分支

我们推荐直接将文档放在 `docs/` 目录下，在设置页面开启 **GitHub Pages** 功能并选择 `master branch /docs folder` 选项。

[![github pages](https://github.com/docsifyjs/docs-zh/raw/_images/deploy-github-pages.png)](https://github.com/docsifyjs/docs-zh/blob/_images/deploy-github-pages.png)

> 可以将文档放在根目录下，然后选择 **master 分支** 作为文档目录。

### GitLab Pages

如果你正在部署你的主分支, 在 `.gitlab-ci.yml` 中包含以下脚本：

> `.public` 的解决方法是这样的，`cp` 不会无限循环的将 `public/` 复制到自身。

```
pages:
  stage: deploy
  script:
  - mkdir .public
  - cp -r * .public
  - mv .public public
  artifacts:
    paths:
    - public
  only:
  - master
```

> 你可以用 `- cp -r docs/. public` 替换脚本, 如果 `./docs` 是你的 docsify 子文件夹。

### VPS

和部署所有静态网站一样，只需将服务器的访问根目录设定为 `index.html` 文件。

例如 nginx 的配置

```
server {
  listen 80;
  server_name  your.domain.com;

  location / {
    alias /path/to/dir/of/docs;
    index index.html;
  }
}
```

### Netlify

1. 登陆你的[Netlify](https://www.netlify.com/)账号
2. 在[dashboard](https://app.netlify.com/)页上点击 **New site from Git**.
3. 选择那个你用来存储文档的git仓库，将 **Build Command** 留空, 将 **Publish directory** 区域填入你的`index.html`所在的目录，例如：填入`docs`(如果你的`index.html`的相对路径是`docs/index.html`的话).

#### HTML5 router

当使用HTML5路由时，你需要设置一条将所有请求重定向到你的`index.html`的重定向规则。当你使用Netlify时这相当简单，在你的**Publish Directory**下创建一个`\redirects`文件，写进以下内容就好了：

```
/*    /index.html   200
```



## 扩展语法

docsify 扩展了一些 Markdown 语法，可以让文档更易读。

#### 强调内容
适合显示重要的提示信息，语法为 !> 内容。

    !> 一段重要的内容，可以和其他 **Markdown** 语法混用。
#### 普通提示信息
普通的提示信息，比如写 TODO 或者参考内容等。

    ?> _TODO_ 完善示例
#### 忽略编译链接
有时候我们会把其他一些相对路径放到链接上，你必须告诉 docsify 你不需要编译这个链接。 例如：

    [link](/demo/)
它将被编译为`<a href="/#/demo/">link</a>`并将加载 /demo/README.md. 可能你想跳转到 /demo/index.html。

现在你可以做到这一点

    [link](/demo/ ':ignore')
即将会得到`<a href="/demo/">link</a>` html 代码。不要担心，你仍然可以为链接设置标题。

    [link](/demo/ ':ignore title')
    <a href="/demo/" title="title">link</a>

#### 设置链接的 target 属性
    [link](/demo ':target=_blank')
    [link](/demo2 ':target=_self')

#### Github 任务列表
    - [ ] foo
    - bar
    - [x] baz
    - [] bam <~ not working
      - [ ] bim
      - [ ] lim

- [ ] foo
bar
- [x] baz
[] bam <~ not working
  - [ ] bim
  - [ ] lim

#### 图片缩放
    ![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
    ![logo](https://docsify.js.org/_media/icon.svg ':size=100')
<img src="https://docsify.js.org/_media/icon.svg" alt="logo" width="50">
<img src="https://docsify.js.org/_media/icon.svg" alt="logo" width="100">

#### 设置标题的 id 属性
    ### 你好，世界！ :id=hello-world



## 兼容 Vue

你可以直接在 Markdown 文件里写 Vue 代码，它将被执行。我们可以用它写一些 Vue 的 Demo 或者示例代码。

### 基础用法

在 `index.html` 里引入 Vue。

```html
<script src="//unpkg.com/vue"></script>
<script src="//unpkg.com/docsify"></script>
```

接着就可以愉快地在 Markdown 里写 Vue 了。默认会执行 `new Vue({ el: '#main' })` 创建示例。

*README.md*

    # Vue 介绍
    
    `v-for`的用法
    
    ```html
    <ul>
      <li v-for="i in 10">{{ i }}</li>
    </ul>
    ```
    
    <ul>
      <li v-for="i in 10">{{ i }}</li>
    </ul>

当然你也可以手动初始化 Vue，这样你可以自定义一些配置。

*README.md*

```markdown
# Vue 的基本用法

<div>hello {{ msg }}</div>

<script>
  new Vue({
    el: '#main',
    data: { msg: 'Vue' }
  })
</script>
```

一个 Markdown 文件里只有第一个 `script` 标签内的内容会被执行。

### 搭配 Vuep 写 Playground

[Vuep](https://github.com/QingWei-Li/vuep) 是一个提供在线编辑和预览效果的 Vue 组件，搭配 docsify 可以直接在文档里写 Vue 的示例代码，支持 Vue component spec 和 JSX。

*index.html*

```html
<!-- inject css file -->
<link rel="stylesheet" href="//unpkg.com/vuep/dist/vuep.css">

<!-- inject javascript file -->
<script src="//unpkg.com/vue"></script>
<script src="//unpkg.com/vuep"></script>
<script src="//unpkg.com/docsify"></script>

<!-- or use the compressed files -->
<script src="//unpkg.com/vue/dist/vue.min.js"></script>
<script src="//unpkg.com/vuep/dist/vuep.min.js"></script>
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
```

*README.md*

```markdown
# Vuep 使用

<vuep template="#example"></vuep>

<script v-pre type="text/x-template" id="example">
  <template>
    <div>Hello, {{ name }}!</div>
  </template>

  <script>
    module.exports = {
      data: function () {
        return { name: 'Vue' }
      }
    }
  </script>
</script>
```

具体效果参考 [Vuep 文档](https://qingwei-li.github.io/vuep/)。


## CDN
推荐使用 unpkg —— 能及时获取到最新版。

### 获取最新版本
根据 UNPKG 的规则，不指定特定版本号时将引入最新版。
```html
<!-- 引入 css -->
<link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">

<!-- 引入 script -->
<script src="//unpkg.com/docsify/lib/docsify.js"></script>
```

### 获取指定版本
如果担心频繁地版本更新又可能引入未知 Bug，我们也可以使用具体的版本。规则是 `//unpkg.com/docsify@VERSION/`
```html
<!-- 引入 css -->
<link rel="stylesheet" href="//unpkg.com/docsify@2.0.0/themes/vue.css">

<!-- 引入 script -->
<script src="//unpkg.com/docsify@2.0.0/lib/docsify.js"></script>
```
> 指定 VERSION 为`latest`可以强制每次都请求最新版本。

### 压缩版
CSS 的压缩文件位于`/lib/themes/`目录下
    <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/vue.css">
JS 的压缩文件是原有文件路径的基础上加`.min`后缀
    <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>

### 其他 CDN
* http://www.bootcdn.cn/docsify (支持国内)
* https://cdn.jsdelivr.net/npm/docsify/ (国内外都支持)
* https://cdnjs.com/libraries/docsify



## 离线模式 PWA

[Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/)(PWA) 是一项融合 Web 和 Native 应用各项优点的解决方案。我们可以利用其支持离线功能的特点，让我们的网站可以在信号差或者离线状态下正常运行。 要使用它也非常容易。

### 创建 serviceWorker

这里已经整理好了一份代码，你只需要在网站根目录下创建一个 `sw.js` 文件，并粘贴下面的代码。

*sw.js*

```js
/* ===========================================================
 * docsify sw.js
 * ===========================================================
 * Copyright 2016 @huxpro
 * Licensed under Apache 2.0
 * Register service worker.
 * ========================================================== */

const RUNTIME = 'docsify'
const HOSTNAME_WHITELIST = [
  self.location.hostname,
  'fonts.gstatic.com',
  'fonts.googleapis.com',
  'unpkg.com'
]

// The Util Function to hack URLs of intercepted requests
const getFixedUrl = (req) => {
  var now = Date.now()
  var url = new URL(req.url)

  // 1. fixed http URL
  // Just keep syncing with location.protocol
  // fetch(httpURL) belongs to active mixed content.
  // And fetch(httpRequest) is not supported yet.
  url.protocol = self.location.protocol

  // 2. add query for caching-busting.
  // Github Pages served with Cache-Control: max-age=600
  // max-age on mutable content is error-prone, with SW life of bugs can even extend.
  // Until cache mode of Fetch API landed, we have to workaround cache-busting with query string.
  // Cache-Control-Bug: https://bugs.chromium.org/p/chromium/issues/detail?id=453190
  if (url.hostname === self.location.hostname) {
    url.search += (url.search ? '&' : '?') + 'cache-bust=' + now
  }
  return url.href
}

/**
 *  @Lifecycle Activate
 *  New one activated when old isnt being used.
 *
 *  waitUntil(): activating ====> activated
 */
self.addEventListener('activate', event => {
  event.waitUntil(self.clients.claim())
})

/**
 *  @Functional Fetch
 *  All network requests are being intercepted here.
 *
 *  void respondWith(Promise<Response> r)
 */
self.addEventListener('fetch', event => {
  // Skip some of cross-origin requests, like those for Google Analytics.
  if (HOSTNAME_WHITELIST.indexOf(new URL(event.request.url).hostname) > -1) {
    // Stale-while-revalidate
    // similar to HTTP's stale-while-revalidate: https://www.mnot.net/blog/2007/12/12/stale
    // Upgrade from Jake's to Surma's: https://gist.github.com/surma/eb441223daaedf880801ad80006389f1
    const cached = caches.match(event.request)
    const fixedUrl = getFixedUrl(event.request)
    const fetched = fetch(fixedUrl, { cache: 'no-store' })
    const fetchedCopy = fetched.then(resp => resp.clone())

    // Call respondWith() with whatever we get first.
    // If the fetch fails (e.g disconnected), wait for the cache.
    // If there’s nothing in cache, wait for the fetch.
    // If neither yields a response, return offline pages.
    event.respondWith(
      Promise.race([fetched.catch(_ => cached), cached])
        .then(resp => resp || fetched)
        .catch(_ => { /* eat any errors */ })
    )

    // Update the cache with the version we fetched (only for ok status)
    event.waitUntil(
      Promise.all([fetchedCopy, caches.open(RUNTIME)])
        .then(([response, cache]) => response.ok && cache.put(event.request, response))
        .catch(_ => { /* eat any errors */ })
    )
  }
})
```

### 注册

现在，到 `index.html` 里注册它。这个功能只能工作在一些现代浏览器上，所以我们需要加个判断。

*index.html*

```html
<script>
  if (typeof navigator.serviceWorker !== 'undefined') {
    navigator.serviceWorker.register('sw.js')
  }
</script>
```

### 体验一下

发布你的网站，并开始享受离线模式的魔力吧！![ghost](https://github.githubassets.com/images/icons/emoji/unicode/1f47b.png) 当然你现在看到的 docsify 的文档网站已经支持离线模式了，你可以关掉 Wi-Fi 体验一下。



## 服务端渲染（SSR）

先看例子 [https://docsify.now.sh](https://docsify.now.sh/)

项目地址在 https://github.com/docsifyjs/docsify-ssr-demo

文档依旧是部署在 GitHub Pages 上，Node 服务部署在 now.sh 里，渲染的内容是从 GitHub Pages 上同步过来的。所以静态部署文档的服务器和服务端渲染的 Node 服务器是分开的，也就是说你还是可以用之前的方式更新文档，并不需要每次都部署。

### 快速开始

如果你熟悉 `now` 的使用，接下来的介绍就很简单了。先创建一个新项目，并安装 `now` 和 `docsify-cli`。

```shell
mkdir my-ssr-demo && cd my-ssr-demo
npm init -y
npm i now docsify-cli -D
```

配置 `package.json`

```json
{
  "scripts": {
    "start": "docsify start .",
    "deploy": "now -p"
  },
  "docsify": {
    "config": {
      "basePath": "https://docsify.js.org/",
      "loadSidebar": true,
      "loadNavbar": true
    }
  }
}
```

如果你还没有创建文档，可以参考[之前的文章](https://zhuanlan.zhihu.com/p/24540753)。其中 `basePath` 为文档所在的路径，可以填你的 docsify 文档网站。

配置可以单独写在配置文件内，然后通过 `--config config.js` 加载。

渲染的基础模版也可以自定义，配置在 `template` 属性上，例如

```html
"docsify": {
    "template": "./ssr.html",
    "config": {
      "basePath": "https://docsify.js.org/",
      "loadSidebar": true,
      "loadNavbar": true
    }
  }
```

*ssr.html*

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>docsify</title>
  <link rel="icon" href="_media/favicon.ico">
  <meta name="keywords" content="doc,docs,documentation,gitbook,creator,generator,github,jekyll,github-pages">
  <meta name="description" content="A magical documentation generator.">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <link rel="stylesheet" href="//unpkg.com/docsify/lib/themes/vue.css" title="vue">
</head>
<body>
  <!--inject-app-->
  <!--inject-config-->
</body>
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
<script src="//unpkg.com/docsify/lib/plugins/search.min.js"></script>
</html>
```

其中 `<!--inject-app-->` 和 `<!--inject-config-->` 为占位符，会自动将渲染后的 html 和配置内容注入到页面上。

现在，你可以运行 `npm start` 预览效果，如果没有问题就通过 `npm run deploy` 部署服务。

```shell
npm start
# open http://localhost:4000

npm run deploy
# now ...
```

### 更多玩法

`docsify start` 其实是依赖了 [`docsify-server-renderer`](https://npmarket.surge.sh/?name=docsify-server-renderer) 模块，如果你感兴趣，你完全可以用它自己实现一个 server，可以加入缓存等功能。

```
var Renderer = require('docsify-server-renderer')
var readFileSync = require('fs').readFileSync

// init
var renderer = new Renderer({
  template: readFileSync('./docs/index.template.html', 'utf-8').,
  config: {
    name: 'docsify',
    repo: 'docsifyjs/docsify'
  }
})

renderer.renderToString(url)
  .then(html => {})
  .catch(err => {})
```

当然文档文件和 server 也是可以部署在一起的，`basePath` 不是一个 URL 的话就会当做文件路径处理，也就是从服务器上加载资源。



## 文件嵌入

docsify 4.6 开始支持嵌入任何类型的文件到文档里。你可以将文件当成 `iframe`、`video`、`audio` 或者 `code block`，如果是 Markdown 文件，甚至可以直接插入到当前文档里。

这是一个嵌入 Markdown 文件的例子。

```
[filename](../_media/example.md ':include')
```

`example.md` 文件的内容将会直接显示在这里(非docsify显示不了)

[filename](../_media/example.md  ':include')

你可以查看 [example.md](../_media/example.md) 原始内容对比效果。

通常情况下，这样的语法将会被当作链接处理。但是在 docsify 里，如果你添加一个 `:include` 选项，它就会被当作文件嵌入。

### 嵌入的类型

当前，嵌入的类型是通过文件后缀自动识别的，这是目前支持的类型：

- **iframe** `.html`, `.htm`
- **markdown** `.markdown`, `.md`
- **audio** `.mp3`
- **video** `.mp4`, `.ogg`
- **code** other file extension

当然，你也可以强制设置嵌入类型。例如你想将 Markdown 文件当作一个 `code block` 嵌入。

```
[filename](../_media/example.md ':include :type=code')
```

你将得到(非docsify显示不了)

[filename](../_media/example.md ':include :type=code')

### 标签属性

如果你嵌入文件是一个 `iframe`、`audio` 或者 `video`，你可以给这些标签设置属性。

```
[Baidu website](https://www.baidu.com ':include :type=iframe width=50% height=400px')
```

[Baidu website](https://www.baidu.com ':include :type=iframe width=50% height=400px')

看见没？你只需要直接写属性就好了，每个标签有哪些属性建议你查看 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)。

### 代码块高亮

如果是嵌入一个代码块，你可以设置高亮的语言，或者让它自动识别。这里是手动设置高亮语言

```
[](../_media/example.html ':include :type=code text')
```

如何高亮代码？你可以查看[这份文档](https://github.com/docsifyjs/docs-zh/blob/master/language-highlight.md).


