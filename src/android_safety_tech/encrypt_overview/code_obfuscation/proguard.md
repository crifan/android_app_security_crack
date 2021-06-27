# ProGuard

## ProGuard的作用

* 压缩=Shrinking
  * 移除未被使用的类、属性、方法等，并且会在优化动作执行之后再次执行（因为优化后可能会再次暴露一些未被使用的类和成员
* 优化=Optimization
  * 优化字节码，并删除未使用的结构
* 混淆=Obfuscation
  * 将类名、属性名、方法名混淆为难以读懂的字母，比如a,b,c等，增大反编译难度

## ProGuard的输出文件说明

* `dump.txt`：说明 APK 中所有类文件的内部结构
* `mapping.txt`：提供原始与混淆过的类、方法和字段名称之间的转换和对应关系
* `seeds.txt`：列出未进行混淆的类和成员
* `usage.txt`：列出从 APK 移除的代码

## 注意事项

* 有些库，混淆后，导致代码不可用
  * 所以有些好的库，专门支持了ProGuard
    * 举例
      * `okhttp`
        * GitHub
          * https://github.com/square/okhttp
            * If you are using R8 or ProGuard add the options from okhttp3.pro
              * [R8 proguard - OkHttp](https://square.github.io/okhttp/r8_proguard/)
  * 有些库不够好，需要自己额外处理
    * 举例
      * PermissionGen
        * https://github.com/lovedise/PermissionGen
          * [某人](https://blog.csdn.net/dobiman/article/details/78595709)：打包混淆以后就废了，需要自己加配置，避免部分模块被混淆，才勉强可用
