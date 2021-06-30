# drizzleDumper

听[别人](https://www.jianshu.com/p/b20ff2ea37f4)提到过，自己没用过。

* 功能
  * 一款基于内存搜索的Android脱壳工具
    * 可以从运行中的安卓app中，利用`ptrace机制`，导出dex文件
* github主页
  * [DrizzleRisk/drizzleDumper: drizzleDumper是一款基于内存搜索的Android脱壳工具](https://github.com/DrizzleRisk/drizzleDumper)
* 机制和原理
  * root设备之后，通过ptrace附加需要脱壳的apk进程，然后在脱壳的apk进程的内存中进行dex文件的特征搜索，当搜索到dex文件时，进行dex文件的内存dump
* 使用步骤
  * 将`\armeabi`下的`drizzleDumper`去`push`进手机
  * 进入`shell`，赋给可执行权限
  * 运行`drizzleDumper [包名] [等待时间,默认为0]`
  * 运行需要脱壳程序
* 使用举例
  ```bash
  $>adb push F:\drizzleDumper /data/local/tmp
  $>chmod 755 drizzleDumper
  $>./drizzleDumper xyz.sysorem.crackme
  ```
