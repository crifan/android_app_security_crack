# 从app导出dex

下面整理关于从`运行中的安卓app`导出`dex`文件的一些`hook`工具。

## 从app导出dex的文件的命名

折腾`FDex2`等工具，从运行中的app导出`dex`文件时，看到很多文件名都是类似于

`com.huili.readingclub8825612.dex`

对这类文件名，并没注意到有何特别。

后来从别人的帖子中，突然意识到：

这些hook工具的生成dex的代码中，对应的命名规则应该是：

`packageName` + `fileSize`.dex

所以此处的

`com.huili.readingclub8825612.dex`

对应着就是：

* `packageName`：`com.huili.readingclub`
* `fileSize`：`8825612`
  * =`8.4MB`
    * 就是dex文件本身的大小
