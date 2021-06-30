# dex文件

## 什么是dex文件

简答：

* `dex` = `Dalvik EXecutable format`=`dex文件`=`dex格式`
  * `dex`之于`Android`，类似于`class`之于`Java`
    * 注：java的class文件内部是Java的字节码(Java bytecode)
    * `dex`=`Dalvik EXecutable`
      * 相关：`dex文件`=`dex字节码`
      * `dex`反汇编后是：`Smali代码`
        * 即：Android（虚拟机中的dex文件）反汇编（后的）代码：`Smali`
  * 文档
    * dex格式
      * Dalvik 可执行文件格式  |  Android 开源项目  |  Android Open Source Project
        * https://source.android.com/devices/tech/dalvik/dex-format
    * 字节码
      * Dalvik 字节码  |  Android 开源项目  |  Android Open Source Project
        * https://source.android.com/devices/tech/dalvik/dalvik-bytecode

详解：

安卓系统中，用`Dalvik虚拟机`(`DVM`=`Dalvik Virtual Machine`)去把`java`源码编译为`dex`可执行文件(Dalvik Executable)。

而dex文件中保存的就是：编译后了的安卓程序代码文件

## Dex文件内部格式

1. File Header
2. String Table
3. Class List
4. Field Table
5. Method Table
6. Class Definition Table
7. Field List
8. Method List
9. Code Header10. Local Variable List


## 相关工具

Android自带`dexdump`：用来反编译`dex`文件
