# 安卓虚拟机

* 历史背景
  * Android
    * 代码语言：`Java`
      * `Java`的虚拟机是：`JVM`
  * Android：出于性能考虑，没用`JVM`，用了自己的虚拟机`VM`
* `安卓虚拟机`=`Android虚拟机`=`Android VM`
  * 旧：`Android < 5.0`：`Dalvik`
    * `Dalvik VM`=`DVM`
      * 概述
        * `Dalvik`是`google`专门为`Android`操作系统设计的一个虚拟机，经过**深度的优化**。虽然Android上的程序是使用java来开发的，但是Dalvik和标准的java虚拟机JVM还是两回事
  * 新：`Android >= 5.0`：`ART`
    * `ART`=`Android RunTime`
* 资料
  * 官网
    * Android Runtime (ART) 和 Dalvik  |  Android 开源项目
      * https://source.android.com/devices/tech/dalvik
