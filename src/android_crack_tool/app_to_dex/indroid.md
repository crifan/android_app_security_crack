# InDroid

* 主页
  * [romangol/InDroid: Dalvik vm Instrumentation OS](https://github.com/romangol/InDroid)
* 作者
  * GoSSIP小组
* 功能
  * 基于Dalvik VM的插桩分析框架
* 原理
  * 直接修改AOSP上的Dalvik VM解释器，在解释器解释执行Dalvik字节码时，插入监控的代码，这样就可以获取到所有程序运行于Dalvik上的动态信息，如执行的指令、调用的方法信息、参数返回值、各种Java对象的数据等等。InDroid只需要修改AOSP的dalvik vm部分代码，编译之后，可直接将编译生成的新libdvm.so刷入任何AOSP支持的真机设备上
