## 发布至 GitHub Pages

在本地git目录下执行：

```shell
mkdocs gh-deploy
```

本地先启动查看：

```shell
mkdocs serve
```

## Installation & Upgrading

mkdocs installation:

```shell
pip install mkdocs
```

mkdocs upgrading:

```shell
pip install -U mkdocs
```

mkdocs-material 模板 installation:

```shell
pip install mkdocs-material
```

mkdocs-material 模板 upgrading:

```shell
pip install --upgrade --force-reinstall mkdocs-material
```

## 构建和预览项目

Create a new project:

```shell
mkdocs new [dir-name]
```

已有项目想本地预览，则直接cd到含mkdocs.yml的目录：

```shell
cd [dir-name]
```

Start the live-reloading docs server:

```shell
mkdocs serve
```

Print help message and exit:

```shell
mkdocs -h
```

本地预览入口：[http://127.0.0.1:8000/](http://127.0.0.1:8000/)

## Project layout

```
mkdocs.yml    # The configuration file.
docs/
	index.md  # The documentation homepage.
	...       # Other markdown pages, images and other files.
```

## mkdocs层级关系

一个 `.md` 里只能有一个 `#`（h1），下面是多个 `##`。

如果有多个 `#`（h1），则是不标准的目录结构，不会自动生产目录。

如果 `.md` 没有用 `#`（h1），则mkdocs会自动将该文件在mkdocs.yml里对应的page名用h1效果展示在第一行。

## 数学公式支持

用于TeX数学公式的展示，使用之前要先在 `docs/` 里创建用于存储 javascripts 脚本的目录，并在目录中放置用于数学渲染的 js 脚本文件。

我的习惯是，存储js脚本的文件夹命名为 `_javascripts`

<span style="background:#FFFFBB;">这意味着每新建一个项目后都要重新配置。</span>

### 第三方方法

`docs/_javascripts/extra.js` 文件：

```javascript
window.MathJax = {
  tex2jax: {
    inlineMath: [ ["\\(","\\)"] ],
    displayMath: [ ["\\[","\\]"] ]
  },
  TeX: {
    TagSide: "right",
    TagIndent: ".8em",
    MultLineWidth: "85%",
    equationNumbers: {
      autoNumber: "AMS",
    },
    unicode: {
      fonts: "STIXGeneral,'Arial Unicode MS'"
    }
  },
  displayAlign: "left",
  showProcessingMessages: false,
  messageStyle: "none"
};
```

然后在 `mkdocs.yml` 里添加如下内容，用于导入js：

```yaml
extra_javascript:
    - '_javascripts/extra.js'
    - 'https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-MML-AM_CHTML'
```

### Material for MkDocs 模板的官方方法

通过 MathJax 渲染块和内联块方程。

`docs/_javascripts/extra.js` 文件：

```javascript
window.MathJax = {
  tex: {
    inlineMath: [["\\(", "\\)"]],
    displayMath: [["\\[", "\\]"]],
    processEscapes: true,
    processEnvironments: true
  },
  options: {
    ignoreHtmlClass: ".*|",
    processHtmlClass: "arithmatex"
  }
};

document$.subscribe(() => { 
  MathJax.typesetPromise()
})
```

配置文件中加入：

```yaml
markdown_extensions:
  # material模板官方数学配置
  - pymdownx.arithmatex:
      generic: true

# 数学公式支持，需要额外的js，现在使用的material模板官方配置
extra_javascript:
  - _javascripts/mathjax.js
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
```

### TeX渲染测试

行间公式：

$$
e^{ix} = \cos x + i\sin x
$$

行内公式：$E = mc^2$

> **注意：数学公式渲染失败大概率是由于语法不规范，记住行间公式 `$$` 前后要空行，不能连着（在Typora中，前后行文字与 `$$` 连着数学公式也是能渲染出来的，但mkdocs不行）**
>
> **有时加载不出数学公式，刷新一下就好**

## 中文搜索支持

需要 `jieba` 库，如果没有则先安装：

```shell
pip install jieba
```

启用：

```yaml
# 插件
plugins:
  - search:
      separator: '[\s\u200b\-]'  # 中文搜索支持
```

## 无序列表 & 任务列表

启用：

```yaml
markdown_extensions:
  - def_list  # 定义列表
  - pymdownx.tasklist:  # 定义任务列表
      custom_checkbox: true
```

使用时，二级必须缩进一个 `Tab` 才能渲染成功，Typora缩进空格就行，注意差异。

任务列表测试：

- [x] MATLAB
- [ ] Python
    - [x] Matplotlab
    - [ ] Tensorflow
- [ ] SQL

## Installing & Using Plugins

在使用插件之前，它必须安装在系统上，如果是第三方插件，则需要先使用 `pip` 安装： 

```shell
pip install mkdocs-foo-plugin
```

使用举例：

```yaml
plugins:
    - search:
        lang: en
        foo: bar
```

具体插件配置请参考插件文档。

## Links

[MkDocs 官网](https://www.mkdocs.org/)

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

[mkdocs/mkdocs Wiki](https://github.com/mkdocs/mkdocs/wiki)

[MkDocs Plugins · mkdocs/mkdocs Wiki](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins)

[MkDocs Themes · mkdocs/mkdocs Wiki](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes)

[pawamoy/best-of-mkdocs：很棒的 MkDocs 项目和插件](https://github.com/pawamoy/best-of-mkdocs)

[danielfrg/mkdocs-jupyter：在 MKDocs 中使用 Jupyter Notebook](https://github.com/danielfrg/mkdocs-jupyter)

[unverbuggt/mkdocs-encryptcontent-plugin：使用 AES 加密/解密 markdown 内容的 MkDocs 插件](https://github.com/unverbuggt/mkdocs-encryptcontent-plugin)

[byrnereese/mkdocs-minify-plugin：用于在将页面写入磁盘之前缩小页面的 MkDocs 插件](https://github.com/byrnereese/mkdocs-minify-plugin)

[Building for offline usage - Material for MkDocs](https://squidfunk.github.io/mkdocs-material/setup/building-for-offline-usage/#built-in-offline-plugin)