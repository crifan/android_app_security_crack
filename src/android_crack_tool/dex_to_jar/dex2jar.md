# dex2jar

## 主页

* 官网
  * [dex2jar | Penetration Testing Tools](https://tools.kali.org/reverse-engineering/dex2jar)
* 其他主页/镜像
  * github
    * [pxb1988/dex2jar: Tools to work with android .dex and java .class files](https://github.com/pxb1988/dex2jar)
  * BitBucket
    * https://bitbucket.org/pxb1988/dex2jar
  * SourceForge
    * https://sourceforge.net/p/dex2jar
  * Google Code
    * https://code.google.com/p/dex2jar

## 功能

* 用于处理`安卓`的`.dex`文件和`java`的`.class`文件的一系列的工具
  * 核心和常用功能
    * 从`dex`文件导出`jar`文件
  * 一系列的工具，包括
    * `dex-reader/writer`: 读写`dex`（Dalvik Executable）文件
      * 具有和`ASM`类似的轻量级的API接口
    * `d2j-dex2jar`: 把`dex`文件转换为`class`文件（=jar压缩包文件=`jar`包=`jar`文件）
    * `smali/baksmali`: 反汇编`dex`转换出`smali`文件, `从smali`文件中汇编出`dex`文件
      * 和[smali/baksmali](https://github.com/JesusFreke/smali)虽然语法相同，但不太一样的是，此处支持描述中包含`"Lcom/dex2jar\t\u1234;"`这类文字描述
    * 其他一些工具
      * [d2j-decrypt-string](https://sourceforge.net/p/dex2jar/wiki/DecryptStrings)

## 用法和举例

用法：

```bash
d2j-dex2jar.sh -f apk_file.apk/dex_file.dex
```

即：

* 从`apk`中转换出`jar`
  ```bash
  sh dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f apk_to_decompile.apk
  ```
* 从`dex`中转换出`jar`
  ```bash
  sh dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f dex_to_decompile.dex
  ```

更详细的用法，详见前面章节

[2.2.1 dex转换出jar · 安卓应用的安全和破解](https://book.crifan.com/books/android_app_security_crack/website/android_crack_tech/how_apk_to_java_src/2_or_3_steps/2_2_1_dex_to_jar.html)
