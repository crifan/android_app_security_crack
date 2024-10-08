# 概述

> [!Warning|title:不准把技术用于非法用途]
> 警告⚠️：相关的安卓逆向破解技术仅限于技术研究使用，**不准**用于**非法目的**，否则后果自负。

先后接触过一些安卓app的逆向破解，现去整理出相关安卓app的安全和逆向相关知识。

关于安卓，大体可以分为**正向的安全**和**逆向的破解**这两大分支：

* 安卓
  * **正向**=**安全**
    * 防静态分析
      * 防砸壳：加壳=加固
        * 加固手段的发展历史
      * 防反编译
        * 代码混淆
          * `Proguard`
          * `Ollvm`
    * 防动态调试
      * 防调试和运行
        * 反调试
        * Root检测
          * 检测`Xposed`、`Frida`等
      * 防抓包=反抓包
        * `ssl pinning`=`证书绑定`
  * **逆向**=**破解**
    * 静态分析
      * 按文件格式类型分
        * 针对`apk`
          * 查看apk信息
            * `aapt`
          * 解包工具：输出`dex`、`so`、`smali`
            * `apktool`
          * 反编译工具
            * 直接apk转java
              * `jadx`
              * `JEB`
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
