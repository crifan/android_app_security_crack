# Cydia Substrate

* 主页
  * [Cydia Substrate](http://www.cydiasubstrate.com)
* 下载
  * [com.saurik.substrate.apk](http://www.cydiasubstrate.com/download/com.saurik.substrate.apk)
* 功能
  * 和`Xposed`类似的框架，用来安装各种插件，实现各种功能。
    * 比如可以：
      * 安装绕过ssl检测的插件，用来破解`ssl pinning`
        * 关于安卓的app中的https：
          * app内部启用了：
            * `SSL Pinning`=`ssl certificate pinning`=`certificate pinning`
              * =`ssl证书绑定`=证书绑定`
      * 此处也可以用来安装相关插件，导出安卓的dex文件
* 特点
  * Hook底层方法非常方便
    * 对so中的方法hook操作非常便捷
* 截图
  * ![](../../../assets/img/cydia_substrate_app_ui.jpg)
