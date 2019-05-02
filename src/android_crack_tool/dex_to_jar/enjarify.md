# Enjarify

* 主页
  * Github
    * 旧：[google/enjarify](https://github.com/google/enjarify)
    * 新：[Storyyeller/enjarify](https://github.com/Storyyeller/enjarify)
* 下载
  * [Releases · Storyyeller/enjarify](https://github.com/Storyyeller/enjarify/releases)
* 功能
  * 把安卓的`Dalvik`字节码转换为Java的`字节码`
    * 和`dex2jar`类似
* 特点
  * Google 官方开源的
  * 用`Python 3`写的
  * 比`dex2jar`更新且更好
* 用法
  * `python3 -O -m enjarify.main yourapp.apk`
  * 已设置好环境变量后
    * `enjarify yourapp.apk`
    * `enjarify classes2.dex`
    * `enjarify yourapp.apk -o yourapp.jar`

## 为何不用`dex2jar`?

* `dex2jar`
  * 比较旧了
  * 大部分情况是转换没问题
  * 但是
    * 有时候
      * 模糊特性时
      * 边缘情况时
    * 转换
      * 会报错
      * 甚至不报错但生成的是错误的结果
* `Enjarify`
  * 最新设计的工具
  * 支持绝大多数（尽可能多的）情况
    * 包括有些dex2jar会出错的情况
    * 且额外支持
      * Unicode的类名
      * 用作多种类型的常量
      * 隐式转换
      * 正常执行流程中的异常处理
      * 引用了非常多的常量的类
      * 名字非常长的方法
      * 捕获函数后的异常处理
      * 错误类型的静态初始变量