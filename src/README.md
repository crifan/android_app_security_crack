# 安卓应用的安全和破解

* 最新版本：`v2.9`
* 更新时间：`20221030`

## 简介

总结安卓应用的安全措施和如何出于研究目的去破解安卓应用，其中介绍好多代的加密技术发展历史，包括常见的代码混淆，自我校验，dex文件变形，dex文件隐藏、so保护等等。总结了安卓的编译和反编译的基本流程和逻辑。整理了加密和解密，反编译，加固，脱壳等相关的工具和技术。典型的反编译流程包括，如何从apk反编译得到java源代码，如何从apk转换出dex文件，如何从dex文件转换出jar文件，如何从jar文件转换出java源代码等等原理和详细步骤。且总结了和安卓反编译、逆向工程、分析等相关的各种工具和软件，包括好用的jadx、Procyon、FDex2、DumpDex、dex2jar、jd-gui、apktool等常用破解工具。以及更新了各个子教程，Android逆向开发、Android逆向：动态调试、Android逆向：重新打包apk等。

## 源码+浏览+下载

本书的各种源码、在线浏览地址、多种格式文件下载如下：

### HonKit源码

* [crifan/android_app_security_crack: 安卓应用的安全和破解](https://github.com/crifan/android_app_security_crack)

#### 如何使用此HonKit源码去生成发布为电子书

详见：[crifan/honkit_template: demo how to use crifan honkit template and demo](https://github.com/crifan/honkit_template)

### 在线浏览

* [安卓应用的安全和破解 book.crifan.org](https://book.crifan.org/books/android_app_security_crack/website)
* [安卓应用的安全和破解 crifan.github.io](https://crifan.github.io/android_app_security_crack/website)

### 离线下载阅读

* [安卓应用的安全和破解 PDF](https://book.crifan.org/books/android_app_security_crack/pdf/android_app_security_crack.pdf)
* [安卓应用的安全和破解 ePub](https://book.crifan.org/books/android_app_security_crack/epub/android_app_security_crack.epub)
* [安卓应用的安全和破解 Mobi](https://book.crifan.org/books/android_app_security_crack/mobi/android_app_security_crack.mobi)

## 版权和用途说明

此电子书教程的全部内容，如无特别说明，均为本人原创。其中部分内容参考自网络，均已备注了出处。如发现有侵权，请通过邮箱联系我 `admin 艾特 crifan.com`，我会尽快删除。谢谢合作。

各种技术类教程，仅作为学习和研究使用。请勿用于任何非法用途。如有非法用途，均与本人无关。

## 鸣谢

感谢我的老婆**陈雪**的包容理解和悉心照料，才使得我`crifan`有更多精力去专注技术专研和整理归纳出这些电子书和技术教程，特此鸣谢。

## 更多其他电子书

本人`crifan`还写了其他`150+`本电子书教程，感兴趣可移步至：

[crifan/crifan_ebook_readme: Crifan的电子书的使用说明](https://github.com/crifan/crifan_ebook_readme)
