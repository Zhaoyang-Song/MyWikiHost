## 发布至 GitHub Pages

在本地git目录下执行

```cmd
mkdocs gh-deploy
```

## 构建和预览项目

```cmd
mkdocs new yourProjectName
cd yourProjectName
mkdocs serve

# 已有项目想本地预览，则直接cd到含mkdocs.yml的目录
mkdocs serve
```

本地预览入口：[http://127.0.0.1:8000/](http://127.0.0.1:8000/)

## mkdocs层级关系

一个 `.md` 里只能有一个 `#`（h1），下面是多个 `##`。

如果有多个 `#`（h1），则是不标准的目录结构，不会自动生产目录。

如果 `.md` 没有用 `#`（h1），则mkdocs会自动将该文件在mkdocs.yml里对应的page名用h1效果展示在第一行。

## 数学公式支持

用于TeX数学公式的展示，使用之前要先在docs/里创建javascripts目录，并在目录中放置extra.js。这意味着每新建一个项目后都要重新配置！

我的习惯是，新建文件夹命名为 `_javascripts`

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

然后在mkdocs.yml里添加如下内容，用于导入js：

```yaml
extra_javascript:
    - '_javascripts/extra.js'
    - 'https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-MML-AM_CHTML'
```

测试一下行间公式：

$$
e^{ix} = \cos x + i\sin x
$$

行内公式：$E = mc^2$

> **注意：有时发现数学公式渲染失败，大概率是由于语法不规范，记住行间公式 `$$` 前后要空行，不能连着（在Typora中，连着数学公式也是能渲染出来的，但mkdocs不行）**
