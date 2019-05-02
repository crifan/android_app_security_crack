# 反编译器

此处主要讨论java反编译器，更主要是的和安卓相关的java的反编译器，其中尤其涉及到dex转出jar包后的，如何从jar包反编译出java源代码的相关反编译器。

## 作用

* 从`jar文件`=`jar包`转换出`java源代码`
  * 用于
    * 在GUI图形界面工具中查看java代码
    * 命令行工具中直接导出整个项目所有的java代码文件

## 总体结论

* 网上目前提到的最多的要数：`JD-GUI`
* 自己的经验和心得
  * `JD-GUI`不太够用：
    * 有些文件转换会出错
    * 且代码逻辑也不够清晰
  * 目前自己
    * 以后尽量用`Jadx`
      * 特点
        * 代码转换不仅不出错
        * 关键是代码逻辑更加清晰和易懂
          * 大大提升代码质量，使得代码更加易读
      * 用来
        * 直接用jadx打开未加固的apk
          * 即可查看和导出java源代码
        * 打开（用FDex2从加固了的apk导出的）dex文件
          * 查看和导出java源代码
    * 其次考虑用：`Procyon`
      * 或基于Procyon的GUI工具：`Luyten`
      * 特点
        * 代码转换不出错的
      * 用来
        * 查看代码：用基于Procyon的Luyten去查看代码
        * 导出代码：用Procyon去从jar反编译转换出java源代码

## 常用安卓相关java反编译器

网上有很多安卓相关的java反编译器，大致整理如下：

* 比较老旧的
  * Jad
    * 不再维护了，源码仓库已关闭
    * 不支持Java 5+
  * Java DeObfuscator
    * https://sourceforge.net/projects/jdo/
    * JDO is a Java DeObfuscator that works on class files directly. JDO contains a simple and easy to use GUI that makes automatic deobfuscation of Java projects a one-click operation!
  * JODE
    * http://jode.sourceforge.net/
    * a java package containing a decompiler and an optimizer for Java. This package is freely available under the GNU GPL. It hasn’t been updated for quite some time.
  * AndroChef
    * http://www.androiddecompiler.com/
    * =
    * http://www.neshkov.com/ac_decompiler.html
    * 只支持Windows平台
  * Candle
    * https://github.com/bradsdavis/candle-decompiler
    * by Brad Davis, developer of JBoss Cake, is an early but promising work in progress= is far away from being feature complete
* 相对新的工具
  * JD-GUI
    * 官网地址：
      * http://jd.benow.ca/
      * -》
      * http://java-decompiler.github.io
    * is an Decompiler, which comes with its own GUI. All is licensed under GPLv3. Like CFR the source for the decompiler itself, is not published, but you have the right to decompile the bionaries. And the binaries are under an OpenSource-License (CFR is under the MIT-license and JD Core is under the GPLv3 license)
    * 转换效果：经常会报错
      * 更准确的说是：对于LINQ/DLR的树编译器产生的代码，会不支持，会报错
        * -》解析后的代码中，包含/* Error */  // Byte code 这种代码
  * CFR
    * 官网
      * CFR - yet another java decompiler.
      * http://www.benf.org/other/cfr/
    * 特点
      * 支持java 9/10/12等
    * by Lee Benfield is well on its way to becoming the premier Java Decompiler. Lee and I actually work for the same company and share regression tests. We're engaged in a friendly competition to see who can deliver a better decompiler. Based on his progress thus far, there's a very good chance he will win--at least on decompiling obfuscated code :).
  * Krakatau
    * https://github.com/Storyyeller/Krakatau
    * by Robert Grosse, written in Python, includes a robust verifier. It focuses on translating arbitrary bytecode into valid Java code, as opposed to reconstructing the original code.
  * Fernflower
    * https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine
    * https://github.com/fesh0r/fernflower
    * an analytical Java decompiler
  * Cavaj
    * https://cavaj-java-decompiler.jaleco.com/
  * Procyon
    * mstrobel / Procyon — Bitbucket
    * https://bitbucket.org/mstrobel/procyon
      * 官网使用文档
        * mstrobel / Procyon / wiki / Java Decompiler — Bitbucket
        * https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler
    * 重点关注Java 5之后的特性支持
      * 这些是其他很多反编译工具不支持的，会报错的
    * 更详细的解释
      * 枚举声明
      * 枚举和字符串的switch表达式
        * 目前只测试支持javac 1.7
      * 局部类Local classes
        * 匿名和带名字的都支持
      * 注解/标注Annotations
      * Java 8的Lambdas和方法引用(比如 :: 操作符)
    * -》对很多人了来说，比较关注：支持java8
    * Procyon本身是命令行工具
    * 基于Procyon的带GUI图形界面的工具
      * SecureTeam Java Decompiler
        * http://www.secureteam.net/Java-Decompiler.aspx
        * A JavaFX-based decompiler front-end with fast and convenient code navigation. Download it, or launch it directly from your browser.
      * Luyten
        * https://github.com/deathmarine/Luyten
        * An open source front-end by deathmarine
      * Bytecode Viewer
        * https://github.com/Konloch/bytecode-viewer
        * -》
        * https://bytecodeviewer.com
        * an open source Java decompilation, disassembly, and debugging suite by @Konloch. It can produce decompiled sources from several modern Java decompilers, including Procyon, CFR, and FernFlower.
      * Helios
        * https://github.com/samczsun/Helios
        * similar to Bytecode Viewer. But is a completely new and independent project, which uses SWT instead of Swing.
      * Enigma
        * http://www.cuchazinteractive.com/enigma/
        * Originally used to deobfuscate Minecraft versions. Uses Procyon internally.
        * 作者已不再维护
  * Jadx
    * 也支持从jar查看java代码
      * 和导出全部代码
        * 导出方式还有2种
          * 保存全部代码
          * 和以Gradle的方式导出源码
            * 如果打开的是apk文件
            * 则导出了dex对应的java源码外，还有assets等资源和其他文件
            * -》更加利于你得到更接近apk的原始代码的项目结构
      * 同时还支持直接打开apk
        * 查看apk中的各种文件
          * 包括java源代码
