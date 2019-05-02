# jadx

* 主页
  * [skylot/jadx: Dex to Java decompiler](https://github.com/skylot/jadx)
* 功能
  * 从`dex`或`apk`文件中转换出`java`源代码的反编译器
* 两种模式/版本
  * 命令行版本=`command line version`：`jadx`
  * 图形界面版本=`GUI`=`graphical version`：`jadx-gui`=`JadxGUI`
    * -> 注意：很多人往往把`jadx-gui`简称为`jadx`
* 截图
  * ![](../../../assets/img/jadx_gui_screenshot.png)

## `jadx-gui`使用举例

## 用`jadx-gui`导出全部代码

`文件 -> 全部保存`

![](../../../assets/img/jadx_gui_file_save_all.png)

即可下载到：

* 各种资源：`resources`
* 源码：`sources`
  * 其中的`sources`，和`文件 -> 另存为Gradle项目`所导出的代码是一样的

![](../../../assets/img/jadx_exported_resources_sources.png)

其中就有我们希望的app的业务逻辑的代码：

![](../../../assets/img/jadx_sources_app_logic_code.png)

### 从`jadx-gui`打开的结构看出是否加固和是哪家的加固

对于某个安卓的apk，用`jadx-gui`打开不同版本的apk的效果是：

* v1.5
  * ![](../../../assets/img/jadx_gui_open_jar_effect_1_5.png)
* v3.4.8
  * ![](../../../assets/img/jadx_gui_open_jar_effect_3_4_8.png)
* v3.6.9
  * ![](../../../assets/img/jadx_gui_open_jar_effect_3_6_9.png)

-》

可以看出apk是否被加固以及用了何种加固方案：

* `v1.5`：没有被加固
* `v3.4.8`：加固方案 qihoo奇虎360
* `v3.6.9`：加固方案 腾讯乐固legu

## `jadx`的help帮助信息=语法参数

```bash
➜  jadx_cmd_exported /xxx/jadx/jadx-0.9.0/bin/jadx --help

jadx - dex to java decompiler, version: 0.9.0

usage: jadx [options] <input file> (.apk, .dex, .jar or .class)
options:
  -d, --output-dir                    - output directory
  -ds, --output-dir-src               - output directory for sources
  -dr, --output-dir-res               - output directory for resources
  -r, --no-res                        - do not decode resources
  -s, --no-src                        - do not decompile source code
  -e, --export-gradle                 - save as android gradle project
  -j, --threads-count                 - processing threads count (default: 2)
  --show-bad-code                     - show inconsistent code (incorrectly decompiled)
  --no-imports                        - disable use of imports, always write entire package name
  --no-replace-consts                 - don't replace constant value with matching constant field
  --escape-unicode                    - escape non latin characters in strings (with \u)
  --respect-bytecode-access-modifiers - don't change original access modifiers
  --deobf                             - activate deobfuscation
  --deobf-min                         - min length of name, renamed if shorter (default: 3)
  --deobf-max                         - max length of name, renamed if longer (default: 64)
  --deobf-rewrite-cfg                 - force to save deobfuscation map
  --deobf-use-sourcename              - use source file name as class name alias
  --cfg                               - save methods control flow graph to dot file
  --raw-cfg                           - save methods control flow graph (use raw instructions)
  -f, --fallback                      - make simple dump (using goto instead of 'if', 'for', etc)
  -v, --verbose                       - verbose output
  --version                           - print jadx version
  -h, --help                          - print this help
Example:
  jadx -d out classes.dex
```

## 常见问题

## Jadx中如何反混淆`deobfuscation`

此处暂时没有找到，反混淆前后对比效果明显的例子。

暂时只能随便找了个效果不明显的，用于解释如何开启和关闭反混淆。

如下：

不带反混淆：

![](../../../assets/img/jadx_gui_not_enable_deobfuscation.png)

![](../../../assets/img/jadx_gui_a_b_c_name.png)

都是a,b,c,d,j,等变量名

启用反混淆：

![](../../../assets/img/jadx_enable_deobfuscation.png)

之前的gK,io等，就反混淆了：

![](../../../assets/img/jadx_variable_name_better.png)

变量名改为了：f23154a，f23155c，虽然反混淆后的效果很一般，但是至少比a,b,c更容易看懂一些。

### jadx转换出错：java.lang.OutOfMemoryError

如果用`jadx`转换代码期间出错：

```bash
java.lang.OutOfMemoryError: GC overhead limit exceeded
    at jadx.core.dex.visitors.blocksmaker.BlockProcessor.computeDominators(BlockProcessor.java:189)
    at jadx.core.dex.visitors.blocksmaker.BlockProcessor.processBlocksTree(BlockProcessor.java:52)
    at jadx.core.dex.visitors.blocksmaker.BlockProcessor.visit(BlockProcessor.java:42)
    at jadx.core.dex.visitors.DepthTraversal.visit(DepthTraversal.java:27)
    at jadx.core.dex.visitors.DepthTraversal.lambda$visit$1(DepthTraversal.java:14)
    at jadx.core.dex.visitors.DepthTraversal$$Lambda$19/469590976.accept(Unknown Source)
    at java.util.ArrayList.forEach(ArrayList.java:1249)
    at jadx.core.dex.visitors.DepthTraversal.visit(DepthTraversal.java:14)
    at jadx.core.ProcessClass.process(ProcessClass.java:32)
    at jadx.api.JadxDecompiler.processClass(JadxDecompiler.java:292)
    at jadx.api.JavaClass.decompile(JavaClass.java:62)
    at jadx.api.JadxDecompiler.lambda$appendSourcesSave$0(JadxDecompiler.java:200)
    at jadx.api.JadxDecompiler$$Lambda$13/1425454633.run(Unknown Source)
    at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
    at java.lang.Thread.run(Thread.java:745)
...
```

且同时伴有：

* CPU占用率很高
* 内存消耗也很大
  * 比如此处JadxCLI占用了4G的内存
    * ![jadx占用4G内存](../../../../assets/img/jadx_memory_4g.jpg)

就是典型的：`OOM`=`Out Of Memory`的问题了。

解决办法，有两种：

* 增加JVM最大内存
  * 逻辑：修改`jadx`脚本，增大`-Xmx`的值
  * 步骤：
    * 编辑`jadx-0.9.0/bin/jadx`，找到`DEFAULT_JVM_OPTS`的配置，修改其中`-Xmx`的值
    * 比如把此处的
    * `DEFAULT_JVM_OPTS='"-Xms128M" "-Xmx4g"'`
    * 改为：
    * `DEFAULT_JVM_OPTS='"-Xms128M" "-Xmx6g"'`
    * 即表示，把JVM最大内存，从之前的`4G`，增大到`6G`
    * 这样就运行`jadx`使用更多的内存，从而降低或消除`OOM`的问题了
* 减少线程数
  * 逻辑：通过`-j N`，N=1/2之类，减少进程数，从而降低内存占用，减少OOM的概率
  * 步骤：
    * 在命令行运行jadx时，传递`-j`参数，指定线程数，比如
      * `jadx -d output_folder -j 1 your_apk.apk`
  * 缺点：
    * 处理速度会有所降低
      * 因为默认`4`线程处理，反编译等速度会比较快
      * 线程数减少后，反编译等速度可能会有所影响

说明：

* 一般反编译小的不复杂的`apk`或`dex`，不会遇到`OOM`问题
* 反编译比较大型的，比较复杂的`apk`或`dex`，才可能会遇到`OOM`
  * 比如之前 [用jadx反编译马蜂窝](http://www.crifan.com/try_crack_android_apk_mafengwo_to_get_java_sourcecode) 遇到了`OOM`