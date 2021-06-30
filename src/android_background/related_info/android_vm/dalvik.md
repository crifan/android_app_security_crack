# Dalvik

* `Dalvik` = `Dalvik VM` = `DVM`
  * `JVM` vs `DVM`
    * 编译流程对比
      * ![jvm_vs_dvm_flow](../../../assets/img/jvm_vs_dvm_flow.png)
      * ![jvm_vs_dvm_compile](../../../assets/img/jvm_vs_dvm_compile.png)
    * JVM：
      * `基础`：基于栈帧`Stack-based`
      * ·文件格式·：`java字节码`=`java bytecode`
      * 效率：相对低
    * DVM：
      * `基础`：基于寄存器`Register-based`
      * `文件格式`：dex
      * 效率：`DVM`效率比`JVM`高
        * 速度更快，占用空间更少
