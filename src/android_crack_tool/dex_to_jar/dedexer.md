# Dedexer

* 主页
  * [Dedexer user's manual](http://dedexer.sourceforge.net)
* 下载
  * [dedexer - Browse Files at SourceForge.net](https://sourceforge.net/project/showfiles.php?group_id=250112)
* 作用
  * 把dex转换为类似于汇编的格式
    * 目的：从dex文件创建类似于Jasmin的源代码
* 用法
  * `java -jar ddx.jar -o -D -d <destination directory> <source>`
  * `java -jar ddx1.5.jar -o -D -d c:\dex\gen c:\dex\classes.dex`
* 举例

```bash
D:\WINDOWS\system32> 
java -jar ddx1.5.jar -o -D -d c:\dex\gen c:\dex\classes.dex 
Processing com/eoeandroid/market/MarketActivity$2 
Processing com/eoeandroid/market/MarketActivity$1 
```