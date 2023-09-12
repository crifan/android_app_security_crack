# 安卓应用的安全和破解

* 最新版本：`v4.0.0`
* 更新时间：`20230903`

## 简介

总结安卓应用的正向安装和逆向破解；先是安卓正向和逆向的概述；然后是安卓背景知识介绍，包括安卓基本框架、apk编译打包流程、以及相关知识，包括apk文件、dex文件、安卓虚拟机的Dalvik和ART，以及Smali。接着介绍安装正向的加固手段发展历史，包括VMP；以及防静态分析，包括加壳加固，为何要加壳，以及常见的加固服务提供商，和代码混淆的ProGuard和Obfuscator-LLVM，以及防动态调试。然后是安卓逆向破解，以及系列子教程。

## 源码+浏览+下载

本书的各种源码、在线浏览地址、多种格式文件下载如下：

### HonKit源码

* [crifan/android_app_security_crack: 安卓应用的安全和破解](https://github.com/crifan/android_app_security_crack)

#### 如何使用此HonKit源码去生成发布为电子书

详见：[crifan/honkit_template: demo how to use crifan honkit template and demo](https://github.com/crifan/honkit_template)

### 在线浏览

* [安卓应用的安全和破解 book.crifan.org](https://book.crifan.org/books/android_app_security_crack/website/)
* [安卓应用的安全和破解 crifan.github.io](https://crifan.github.io/android_app_security_crack/website/)

### 离线下载阅读

* [安卓应用的安全和破解 PDF](https://book.crifan.org/books/android_app_security_crack/pdf/android_app_security_crack.pdf)
* [安卓应用的安全和破解 ePub](https://book.crifan.org/books/android_app_security_crack/epub/android_app_security_crack.epub)
* [安卓应用的安全和破解 Mobi](https://book.crifan.org/books/android_app_security_crack/mobi/android_app_security_crack.mobi)

## 版权和用途说明

此电子书教程的全部内容，如无特别说明，均为本人原创。其中部分内容参考自网络，均已备注了出处。如发现有侵权，请通过邮箱联系我 `admin 艾特 crifan.com`，我会尽快删除。谢谢合作。

各种技术类教程，仅作为学习和研究使用。请勿用于任何非法用途。如有非法用途，均与本人无关。

## 鸣谢

感谢我的老婆**陈雪**的包容理解和悉心照料，才使得我`crifan`有更多精力去专注技术专研和整理归纳出这些电子书和技术教程，特此鸣谢。

## 其他

### 作者的其他电子书

本人`crifan`还写了其他`150+`本电子书教程，感兴趣可移步至：

[crifan/crifan_ebook_readme: Crifan的电子书的使用说明](https://github.com/crifan/crifan_ebook_readme)

### 关于作者

关于作者更多介绍，详见：

[关于CrifanLi李茂 – 在路上](https://www.crifan.org/about/)
