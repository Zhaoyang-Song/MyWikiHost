## Zotero Better Notes 插件笔记模板配置

[[Item] item-notes with item & Metadata & Comments & Excerpts · Discussion #308 · windingwind/zotero-better-notes](https://github.com/windingwind/zotero-better-notes/discussions/308)

## 笔记Tips：关自动同步

需要提醒一下大家，如果你需要在zotero里面做笔记，最好的自动同步功能取消了。比如，可能你做笔记的时候笔记会自动消失，因为它自动同步的时候，笔记就会退回十几秒之前的状态，把自动同步取消就好了，可以定期手动自动同步一下。（软件右上角的一个绿色类似加载按钮的就是手动同步按钮）

## 不用安装其它软件清理删除条目后残留的PDF方法

[[Zotero]不用安装其它软件清理删除条目后残留的PDF方法](https://zhuanlan.zhihu.com/p/356071795)

**注意：**

**1.附件的清理不可恢复，请提前备份。**

**2.中文目录可能不支持。**

**3.不属于Zotero条目附件的文件不要放在ZotFile的目录中，会被清理。**

在Zotero中依次点击Tools -> Developer -> Run JavaScript，然后复制以下代码到左边的窗口中：

```javascript
var truthBeTold = window.confirm("所有附件的清理不可恢复，单击“确定”继续。单击“取消”停止。")
if (truthBeTold) {
//清理zotfile目录
var AllFiles = []; //现在库中所有的文件
var DirFiles = []; //当前文件夹中的文件
var DelFileNum = 0; //被清理的文件个数
var path = Zotero.ZotFile.getPref("dest_dir")   //得到zotfile目录
var FullPath ='' //文件的完整路径
var OutText="";//供输出的文本，主要用于换行
//得到当前库中的附件
var s = new Zotero.Search();
s.libraryID = Zotero.Libraries.userLibraryID;
var results = await s.search();
var items = await Zotero.Items.getAsync(results);
for (let item of items){
 let file = await getFilePath(item);
  if (file){
    AllFiles.push(OS.Path.basename(file));//只存入文件名
  }
}

//得到ZotFile目录中的文件
await Zotero.File.iterateDirectory(path, async function(entry){
    if (!entry.isDir) {
        DirFiles.push(entry.name);
     }
});

//判断是否在库的文件中
for (let DirFile of DirFiles){
    if (AllFiles.indexOf(DirFile)==-1){
      DelFileNum += 1;//计数器加1
      FullPath = OS.Path.join(path, DirFile);
      OutText += DelFileNum + ": "+ DirFile + "\n" 
      //await OS.File.remove(FullPath); //删除文件
    }
}
alert(DelFileNum + "个文件被清理。\n 被清理的文件：\n" + OutText);
async function getFilePath(item) { //1 函数
  if (item && !item.isNote()) { //2 if
        if (item.isRegularItem()) { // Regular Item 一般条目//3 if 
           let attachmentIDs = item.getAttachments();
            for (let id of attachmentIDs) { //4 for
                var file = await Zotero.Items.get(id).getFilePathAsync();
                return file;
            } //4 for
        } // 3 if
        if (item.isAttachment()) { //附件条目 5 if
                var file = await item.getFilePathAsync();
                return file;
        }//5if
 } //2 if
} 
}
```

可以先将

```javascript
awaitOS.File.remove(FullPath);//删除文件
```

前面加上//，注释掉删除文件的语句，看一下会删除的文件。

只看有哪些附件需要被清理但暂时不删除情况的js代码：

```javascript
var truthBeTold = window.confirm("所有附件的清理不可恢复，单击“确定”继续。单击“取消”停止。")
if (truthBeTold) {
//清理zotfile目录
var AllFiles = []; //现在库中所有的文件
var DirFiles = []; //当前文件夹中的文件
var DelFileNum = 0; //被清理的文件个数
var path = Zotero.ZotFile.getPref("dest_dir")   //得到zotfile目录
var FullPath ='' //文件的完整路径
var OutText="";//供输出的文本，主要用于换行
//得到当前库中的附件
var s = new Zotero.Search();
s.libraryID = Zotero.Libraries.userLibraryID;
var results = await s.search();
var items = await Zotero.Items.getAsync(results);
for (let item of items){
 let file = await getFilePath(item);
  if (file){
    AllFiles.push(OS.Path.basename(file));//只存入文件名
  }
}

//得到ZotFile目录中的文件
await Zotero.File.iterateDirectory(path, async function(entry){
    if (!entry.isDir) {
        DirFiles.push(entry.name);
     }
});

//判断是否在库的文件中
for (let DirFile of DirFiles){
    if (AllFiles.indexOf(DirFile)==-1){
      DelFileNum += 1;//计数器加1
      FullPath = OS.Path.join(path, DirFile);
      OutText += DelFileNum + ": "+ DirFile + "\n" 
      //await OS.File.remove(FullPath); //删除文件
    }
}
alert(DelFileNum + "个文件被清理。\n 被清理的文件：\n" + OutText);
async function getFilePath(item) { //1 函数
  if (item && !item.isNote()) { //2 if
        if (item.isRegularItem()) { // Regular Item 一般条目//3 if 
           let attachmentIDs = item.getAttachments();
            for (let id of attachmentIDs) { //4 for
                var file = await Zotero.Items.get(id).getFilePathAsync();
                return file;
            } //4 for
        } // 3 if
        if (item.isAttachment()) { //附件条目 5 if
                var file = await item.getFilePathAsync();
                return file;
        }//5if
 } //2 if
} 
}
```

## Zotero IF 插件

该插件由“青柠学术”开发，需要去公众号回复获得安装包（作者github上也有号，但还是引流回微信公众号了）

## 插件备份

[bwiernik/zotero-shortdoi - 获取文献的DOI](https://github.com/bwiernik/zotero-shortdoi)

[eschnett/zotero-citationcounts - 获取文献的被引用次数](https://github.com/eschnett/zotero-citationcounts)

## Links

[Zotero CN](https://zotero-cn.github.io/)

[整合 | Zotero文献管理工具配置手册（治愈强迫症）](https://zhuanlan.zhihu.com/p/371968761)

[zotero-plugins-market: 到 Zotero 插件市场，找到你需要的插件](https://gitee.com/qnscholar/zotero-plugins-market)

[Zotero 插件下载](https://zotero-chinese.gitee.io/zotero-plugins/#/)

[translators_CN: Zotero translator中文网页抓取插件](https://github.com/l0o0/translators_CN)

[Zotero 暗黑模式 - Rosmaninho/Zotero-Dark-Theme](https://github.com/Rosmaninho/Zotero-Dark-Theme)
