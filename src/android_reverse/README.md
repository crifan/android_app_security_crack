# 安卓逆向破解

此处主要介绍安卓的逆向破解方面的内容：

## 概述

* 安卓的逆向破解
  * 静态分析
    * 按文件格式类型分
      * 针对`apk`
        * 查看apk信息
          * `aapt`
        * 解包工具：输出`dex`、`so`、`smali`
          * `apktool`
          * `jadx`
        * 反编译工具
          * 直接apk转java
            * `jadx`
            * `GDA`
      * 针对`dex`
        * 各种导出dex的工具=砸壳工具=脱壳工具
          * `FDex2`
          * `DumpDex`
          * `DexExtractor`
        * 各种反编译dex的工具
          * dex转jar
            * `dex2jar`
          * dex转smali
            * `baksmali`
          * dex直接转java
            * `jadx`
            * `GDA`
      * 针对`jar`
        * jar转java=各种反编译工具
          * `jadx`
          * `Procyon`
          * `CFR`
          * `JD-GUI`
      * 针对`so`库文件=（往往是ARM64架构）的ELF文件
        * 导出静态资源
          * `readelf`
          * `objdump`
          * `razbin2`
        * 反编译代码逻辑
          * `IDA`
          * `Hopper`
          * `Radare2`
          * `Ghidra`
    * 涉及子领域
      * 反代码混淆
  * 动态调试
    * （绕过限制去）抓包
      * 绕过证书绑定的Exposed插件或Frida的脚本
    * 反root检测
    * 反反调试
    * 各种动态调试手段
      * 调试smali：`AS+smalidea插件`
        * app进程可调试
          * Magisk插件：`MagiskHide Props Config`
      * 调试Frida：`Frida`
        * Frida环境搭建
          * Magisk插件：`MagiskFrida`
      * 调试lldb：`LLDB`
      * 调试Xposed插件
        * `XPosed`
        * `EdXposed`
        * `LSPosed`
      * 模拟代码执行
        * `Unidbg`
          * `Unicorn`
      * 辅助调试工具
        * `adb`
        * `DDMS`
  * 输出
    * 重新打包apk
      * `apktool`
      * `keytool`
      * `jarsigner`或`apksigner`
      * `zipalign`
    * 用代码重写逻辑
      * Python代码
      * C/C++代码
    * 改机定制ROM
      * `AOSP源码`编译
      * `JNI`开发
      * `NDK`开发

另外：

* 砸壳思路=脱壳方案
  * 目前多数都是基于`Hook`框架，去从安卓app中导出dex文件
    * 典型的hook框架
      * `XPosed`：从根上Hook了Android Java虚拟机
      * `Cydia`：支持jni和java层的HOOK功能
    * 再去从dex中转换出java代码

## 详解

具体内容，详见独立子教程：

[Android逆向开发](https://book.crifan.org/books/android_reverse_dev/website/)
