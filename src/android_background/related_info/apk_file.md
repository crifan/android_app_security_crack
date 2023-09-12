# apk文件

* `apk`=`android Application PacKage`=`APK`
  * apk文件是什么：是安卓app的安装文件
  * 本质：（apk文件其实就是个）zip压缩包
    * 意味着
      * 可以用解压缩工具把apk当做zip文件一样去解压
        * 解压后，得到一堆安卓相关文件
      * 可以在`apktool`等工具破解和修改了安卓文件后，再重新用压缩文件工具或`apktool`等工具，重新打包为`apk`文件

## apk内容结构

| 内容入口 | 含义解释 |
| ------- | ------- |
| AndroidManifest.xml | 二进制xml文件，提供设备运行应用程序所需的各种信息 |
| classes.dex | 以dex格式编译的应用程序代码 |
| resources.arsc | 包含预编译应用程序资源的二进制XML文件 |
| res/ | 此文件夹中包含未编译到resources.arsc文件中的资源 |
| assets/ | 此文件夹包含应用程序的原始资产，由AssetManager提供对这些资产文件的访问 |
| META-INF/ | 它包含MANIFEST.MF文件，该文件存储有关JAR内容的元数据。APK的签名也存储在此文件夹中 |
| lib/ | 该文件夹包含已编译的代码，例如本地代码库 |

## apk产生的大概过程

简述安卓apk的产生过程：

* 概述：`.java`->`.class`->`.dex`->`.apk`
* 详解
  * java源代码
    * `java编译器` 编译
  * class文件
    * `dx`工具转换和打包压缩
      * 加上 第三方的，其他的库文件
  * dex文件
    * apkbuilder打包
      * 加上 其他资源文件resources.arsc，其他库等
  * （未签名的）apk文件
    * jarsigner去签名 + zipalign去处理
  * （已签名的）apk文件
    * 可以用于发布和上架各种安卓应用市场
      * 供普通用户下载安装试用
