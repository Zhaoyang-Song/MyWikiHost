## 快捷键

**选择编译链**：选中tex文件的代码页面（若未选中，则无法进行编译），然后按下 `Ctrl+Alt+R`（该快捷键为自定义的）

**预览编译好的PDF**：选中 tex 文件中任意的代码，然后按 `Ctrl+Alt+V`，出现编译好的 pdf 页面（该快捷键为默认设置）

**正向搜索快捷键**：`Ctrl+Alt+J`（该快捷键为默认设置）

##  VSCode+SumatraPDF进行双向搜索（Win）

VSCode的配置文件 `settings.json` 中添加以下内容：（注意修改其中涉及到的路径以适配本机）

```json
    "latex-workshop.view.pdf.viewer": "external",

    "latex-workshop.view.pdf.external.viewer.command": "C:\\Program Files\\SumatraPDF\\SumatraPDF.exe",
    "latex-workshop.view.pdf.external.viewer.args": [
            "-forward-search",
            "%TEX%",
            "%LINE%",
            "-reuse-instance",
            "%PDF%"
    ], 

    "latex-workshop.view.pdf.external.synctex.command": "C:\\Program Files\\SumatraPDF\\SumatraPDF.exe",
    "latex-workshop.view.pdf.external.synctex.args": [
            "-forward-search",
            "%TEX%",
            "%LINE%",
            "-reuse-instance",
            "%PDF%"
    ]
```

SumatraPDF中，点击 `设置->选项`，在最下面的一栏中填入：（注意修改其中涉及到的路径以适配本机）

````
"C:\Users\roger\AppData\Local\Programs\Microsoft VS Code\Code.exe" "C:\Users\roger\AppData\Local\Programs\Microsoft VS  Code\resources\app\out\cli.js" --ms-enable-electron-run-as-node -r -g  "%f:%l"
````

VSCode的正向搜索快捷键默认的是 `Ctrl+Alt+J`

## Links

[Visual Studio Code (vscode) 配置LaTeX](https://zhuanlan.zhihu.com/p/166523064)

[Latex+VSCode 正向搜索和反向搜索 | Jintao Lee](https://jintaolee-roger.github.io/posts/latexsearch/)