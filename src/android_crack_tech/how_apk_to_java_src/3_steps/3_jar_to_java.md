# 3. jar转换出java

## 准备

* 前面一步从`dex`转换得到的`jar`文件
  * ![com.huili.readingclub8825612-dex2jar.jar](../../../../assets/img/to_decode_jar_file.png)
* 选择合适的反编译器：`jadx`
  * 用于从`jar`转换出`java`源代码
  * 网上很多人提到了用的比较广的：`JD-GUI`
    * 经过实测，基本够用，但不够完美
  * 后续自己测试了多个其他的反编译器
  * 最终结论如下：
    * `Jadx` > `Procyon` > `CFR` > `JD-GUI`
      * 详见：[常见反编译器对比 · 安卓应用的安全和破解](http://book.crifan.com/books/android_app_security_crack/website/android_crack_tool/decompiler/common_decompiler_compare.html)
  * 所以此处选用：`jadx`
* 下载`jadx`
  * 从[这里](https://github.com/skylot/jadx/releases)下载最新版的`jadx`
    * 比如：
      * [jadx-0.9.0.zip](https://github.com/skylot/jadx/releases/download/v0.9.0/jadx-0.9.0.zip)
    * 解压后得到：
      * `jadx`：命令行工具
      * `jadx-gui`：带图形界面的
        * 双击即可运行

## 详细步骤

此处想要用`jadx`去从`jar`中导出代码，有两种方式：

* 用`jadx`的命令行直接导出代码
* 用`jadx-gui`查看代码，也可以再导出代码

下面详细介绍

### `jadx`直接导出代码

切换到要导出代码的目录，已有dex文件要导出，则可以直接运行：

```bash
jadx-0.9.0/bin/jadx to_decode_dex_file.dex -d .
```

即可转换出源代码到当前目录下，输出有：

* resources
* sources
  * 有你要的源码

转换速度还是不错的。

#### 举例

```bash
from_v3.4.8_dex /Users/crifan/dev/dev_tool/android/reverse_engineering/jadx/jadx-0.9.0/bin/jadx ../../../../../xiaohuasheng/app_hook_dump_dex/FDex2/v3.4.8/com.huili.readingclub8825612.dex -d .
...
中间很多错误
...
WARN  - Found 75 references to unknown classes
ERROR - 6 errors occurred in following nodes:
ERROR -   Method: android.support.v4.provider.FontsContractCompat.getFontFromProvider(android.content.Context, android.support.v4.provider.FontRequest, java.lang.String, android.os.CancellationSignal):android.support.v4.provider.FontsContractCompat$FontInfo[]
ERROR -   Method: cn.addapp.pickers.util.LogUtils.getTraceElement():java.lang.String
ERROR -   Method: cn.jiguang.a.a.b.c.a(android.os.Message):void
ERROR -   Method: cn.jiguang.d.b.f.a(int):boolean
ERROR -   Method: cn.jiguang.d.d.m.a(android.content.Context, boolean):java.util.List<java.io.File>
ERROR -   Method: cn.jiguang.g.e.a(java.lang.String, java.util.Map):cn.jiguang.g.e
WARN  - 2299 warnings in 454 nodes
ERROR - finished with errors
```

转换后：

```bash
➜  from_v3.4.8_dex ll
total 0
drwxr-xr-x   3 crifan  staff    96B  4 29 15:29 resources
drwxr-xr-x  13 crifan  staff   416B  4 29 15:30 sources
```

转换后的代码用VSCode去打开的效果：

![](../../../../assets/img/jadx_cli_exported_code.png)

### `jadx-gui`查看和导出代码

双击`jadx-gui`即可运行：

![](../../../../assets/img/jadx_gui_running.png)

然后去打开对应的jar文件：`com.huili.readingclub8825612-dex2jar.jar`，即可看到包含了app业务逻辑的代码结构和包名：

![](../../../../assets/img/jadx_decoded_app_logic_structure.png)

然后展开后可以看到详细的代码：

![](../../../../assets/img/jadx_show_detailed_java_code.png)

然后如果想要导出全部代码，则可以去：

`File -> Save All`

![](../../../../assets/img/jadx_save_all.png)

然后稍等片刻：

![](../../../../assets/img/jadx_exporting_code.png)

即可在导出的`sources`文件夹中找到你要的源码：

![](../../../../assets/img/exported_sources_found_java_src.png)

具体过程详见：

[反编译器 Jadx](http://book.crifan.com/books/android_app_security_crack/website/android_crack_tool/decompiler/common_decompilers/jadx.html)

## 备注和说明

### 用`JD-GUI`打开同一个`jar`的效果

另外，用`JD-GUI`打开同一个jar的效果：

![](../../../../assets/img/jd_gui_open_app_logic_jar.png)

其中找到了我们之前需要的app相关的业务逻辑的代码：

`/com/huili/readingclub/activity/classroom/SelfReadingActivity.class`

![](../../../../assets/img/include_app_logic_selfreadingactivity_code.png)

其中`onSuccess`中就是我们希望得到的对于`J`字段解密的逻辑。

### 其他无效的jar转换出jar的效果

如前一步所说的，从多个`dex`可以转换出多个`jar`

而这些无效的，没有包含app业务逻辑的`jar`，去用一些反编译工具打开，效果是：

![](../../../../assets/img/jd_gui_open_jar_android.png)

其他的一些，比如腾讯乐固加密了的，最终转换出来的jar，去打开后只能看到腾讯乐固的代码：

![](../../../../assets/img/jd_gui_jar_show_tencent_legu.png)