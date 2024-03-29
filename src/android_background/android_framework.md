# 安卓基本框架

为了更好的理解，安卓破解相关知识和工具，先要了解安卓的基本框架，以及每一层中都是什么东西：

## 安卓的基本架构

* 内核层：
  * 支持多进程和多线程的Linux内核
  * 每个应用程序都有自己的Linux ID，并在单独的进程中运行
  * 具有相同ID的两个应用程序可以彼此交换数据。
* 系统运行层
  * 主要包括一些`开源类库`以及`Android运行时环境`
    * 其中虚拟机（`Dalvik`、`ART`）中运行的应用程序格式为`dex`的`二进制文件`
* 应用框架层
  * 具有Java接口的应用程序框架
    * 主要组成
      * `Java`层的`Android SDK`
      * `Native`层的`Android NDK`
* 应用层
  * 预安装一些核心应用程序

后续的很多破解工具，则是针对`Dalvik`虚拟机和dex文件去破解的。
