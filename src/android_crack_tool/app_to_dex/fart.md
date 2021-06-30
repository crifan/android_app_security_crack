# FART

* `FART`
  * 是什么：ART环境下基于主动调用的自动化脱壳方案
  * 特点：支持ART（新安卓的VM虚拟机）
    * 基于Android 6.0实现，理论上可以移植到任何ART系统上
  * FART脱壳的步骤
    * 1.内存中DexFile结构体完整dex的dump
    * 2.主动调用类中的每一个方法，并实现对应CodeItem的dump
    * 3.通过主动调用dump下来的方法的CodeItem进行dex中被抽取的方法的修复
  * 详解
    * hanbinglengyue/FART: ART环境下自动化脱壳方案
      * https://github.com/hanbinglengyue/FART
    * [原创]FART：ART环境下基于主动调用的自动化脱壳方案-Android安全-看雪论坛-安全社区|安全招聘|bbs.pediy.com
      * https://bbs.pediy.com/thread-252630.htm
