# 2. dex转换出jar

## 思路

从前面的`app导出dex`，我们已得到：（一个或）多个dex文件，而这么多`dex`，其中只有一个是真正包含了安卓app的业务逻辑的`dex`文件。

我们后续会（经过转换和尝试而）找到该`dex`，然后用`dex2jar`等工具从`dex`转换出`jar`文件

## 准备

* 下载`dex2jar`
  * 从[dex2jar的下载页面](https://github.com/pxb1988/dex2jar/releases)下载到最新版本的`dex2jar`
    * 比如：[dex-tools-2.1-SNAPSHOT.zip](https://github.com/pxb1988/dex2jar/files/1867564/dex-tools-2.1-SNAPSHOT.zip)
      * 解压后得到：`d2j-dex2jar.sh`

## 详细步骤

比如前面的`v3.4.8`版本的某安卓apk，经过前面一步导出了多个`dex`文件后，此处接着去用`dex2jar`去分别转换出`jar`。

期间，很多个`dex`转换`jar`的期间都会报错。

经过尝试最终找到了，转换不仅不报错且转换出来的`jar`还是我们希望的有效的包含了app业务逻辑的`jar`：

```bash
➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub3986968.dex
dex2jar com.huili.readingclub3986968.dex -> ./com.huili.readingclub3986968-dex2jar.jar
➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub8825612.dex
dex2jar com.huili.readingclub8825612.dex -> ./com.huili.readingclub8825612-dex2jar.jar
```

经后续确定，此处：

* 从：`8.4MB`的`com.huili.readingclub8825612.dex`
* 转换出的：`10MB`的`com.huili.readingclub8825612-dex2jar.jar`

就是我们要的，包含了app的业务逻辑的代码。

## 说明和提示

### apk改名zip解压得到的`classes.dex`去转换一般无法得到有效的`jar`

比如之前的`v3.6.9`版本的某安卓apk，改名为`zip`再解压得到的`classes.dex`，此处用`dex2jar`去转换：

```bash
➜  classes.dex pwd
/Users/crifan/dev/dev_root/company/naturling/projects/crawl_data/小花生app/xiaohuasheng/decoded dex/v3.6.9/classes.dex
➜  classes.dex /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f classes.dex
dex2jar classes.dex -> ./classes-dex2jar.jar
➜  classes.dex ll
total 26000
-rw-------  1 crifan  staff   212K  3 25 10:20 classes-dex2jar.jar
-rwxr-xr-x@ 1 crifan  staff    12M  1 25 17:43 classes.dex
```

虽然转换过程并没有报错，但是才得到200多KB的jar

-》最终经确认，其中没有包含业务逻辑代码，不是我们需要的jar，是无效的jar

### 多个`dex`转换`jar`的期间会报错

比如：

```bash
➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub1166288.dex
...
GLITCH: 0000 Lcom/android/internal/telephony/uicc/VoiceMailConstants;.getVoiceMailTag(Ljava/lang/String;)Ljava/lang/String; | zero-width instruction op=0xf4
Detail Error Information in File ./com.huili.readingclub1166288-error.zip
Please report this file to one of following link if possible (any one).
    https://sourceforge.net/p/dex2jar/tickets/
    https://bitbucket.org/pxb1988/dex2jar/issues
    https://github.com/pxb1988/dex2jar/issues
    dex2jar@googlegroups.com

➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub13088280.dex
...
GLITCH: 009f Lcom/tencent/bugly/legu/proguard/z;.a(Ljava/lang/Thread;Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;)V | zero-width instruction op=0xf8
Detail Error Information in File ./com.huili.readingclub13088280-error.zip


➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub1461452.dex
...
GLITCH: 0000 Lcom/google/android/util/SmileyResources;.getSmileys()Lcom/google/android/util/AbstractMessageParser$TrieNode; | zero-width instruction op=0xf4
WARN: can't get operand(s) for sub-double/2addr, out-of-range or not initialized ?
WARN: can't get operand(s) for int-to-float, out-of-range or not initialized ?
WARN: can't get operand(s) for return-wide, out-of-range or not initialized ?
WARN: can't get operand(s) for move-exception, out-of-range or not initialized ?
WARN: can't get operand(s) for move-exception, out-of-range or not initialized ?
Detail Error Information in File ./com.huili.readingclub1461452-error.zip


➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub191572.dex
...
GLITCH: 0006 Lcom/android/okhttp/internal/tls/OkHostnameVerifier;.verifyHostName(Ljava/lang/String;Ljava/lang/String;)Z | zero-width instruction op=0xee
Detail Error Information in File ./com.huili.readingclub191572-error.zip

➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub2847840.dex
...
GLITCH: 0006 Lsun/misc/Unsafe;.unpark(Ljava/lang/Object;)V | zero-width instruction op=0xf8
Detail Error Information in File ./com.huili.readingclub2847840-error.zip
➜  v3.4.8 /Users/crifan/dev/dev_tool/android/reverse_engineering/dex-tools/dex-tools-2.1-SNAPSHOT/d2j-dex2jar.sh -f com.huili.readingclub8725900.dex
...
GLITCH: 0000 Landroid/widget/ZoomControls;.setOnZoomOutClickListener(Landroid/view/View$OnClickListener;)V | zero-width instruction op=0xf4
GLITCH: 0000 Landroid/widget/ZoomControls;.setZoomSpeed(J)V | zero-width instruction op=0xf4
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-object/16, out-of-range or not initialized ?
WARN: can't get operand(s) for shr-int/2addr, out-of-range or not initialized ?
WARN: can't get operand(s) for move/16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move/16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result, wrong position ?
WARN: can't get operand(s) for cmpl-float, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for sput-boolean, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-object/from16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-object/from16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-object/from16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-object/from16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-object/from16, out-of-range or not initialized ?
WARN: can't get operand(s) for sput-boolean, out-of-range or not initialized ?
WARN: can't get operand(s) for sput-boolean, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for aput-char, out-of-range or not initialized ?
WARN: can't get operand(s) for mul-float, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for move-wide/16, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for mul-int/2addr, out-of-range or not initialized ?
WARN: can't get operand(s) for aput-char, out-of-range or not initialized ?
WARN: can't get operand(s) for aput-char, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for sput-byte, out-of-range or not initialized ?
WARN: can't get operand(s) for aget-byte, out-of-range or not initialized ?
WARN: can't get operand(s) for and-int/2addr, out-of-range or not initialized ?
WARN: can't get operand(s) for move/from16, out-of-range or not initialized ?
WARN: can't get operand(s) for iput-boolean, out-of-range or not initialized ?
WARN: can't get operand(s) for iput-boolean, out-of-range or not initialized ?
WARN: can't get operand(s) for move-result-object, wrong position ?
WARN: can't get operand(s) for cmpg-float, out-of-range or not initialized ?
Detail Error Information in File ./com.huili.readingclub8725900-error.zip
Please report this file to one of following link if possible (any one).
    https://sourceforge.net/p/dex2jar/tickets/
    https://bitbucket.org/pxb1988/dex2jar/issues
    https://github.com/pxb1988/dex2jar/issues
    dex2jar@googlegroups.com
java.util.IllegalFormatConversionException: d != java.lang.String
    at java.util.Formatter$FormatSpecifier.failConversion(Formatter.java:4302)
    at java.util.Formatter$FormatSpecifier.printInteger(Formatter.java:2793)
    at java.util.Formatter$FormatSpecifier.print(Formatter.java:2747)
    at java.util.Formatter.format(Formatter.java:2520)
    at java.util.Formatter.format(Formatter.java:2455)
    at java.lang.String.format(String.java:2940)
    at com.googlecode.d2j.smali.BaksmaliDumpOut.s(BaksmaliDumpOut.java:68)
    at com.googlecode.d2j.smali.BaksmaliCodeDumper.visitFilledNewArrayStmt(BaksmaliCodeDumper.java:248)
    at com.googlecode.d2j.node.insn.FilledNewArrayStmtNode.accept(FilledNewArrayStmtNode.java:19)
    at com.googlecode.d2j.smali.BaksmaliDumper.accept(BaksmaliDumper.java:569)
    at com.googlecode.d2j.smali.BaksmaliDumper.baksmaliCode(BaksmaliDumper.java:544)
    at com.googlecode.d2j.smali.BaksmaliDumper.baksmaliMethod(BaksmaliDumper.java:482)
    at com.googlecode.d2j.smali.BaksmaliDumper.baksmaliMethod(BaksmaliDumper.java:428)
    at com.googlecode.dex2jar.tools.BaksmaliBaseDexExceptionHandler.dumpMethod(BaksmaliBaseDexExceptionHandler.java:148)
    at com.googlecode.dex2jar.tools.BaksmaliBaseDexExceptionHandler.dumpTxt0(BaksmaliBaseDexExceptionHandler.java:126)
    at com.googlecode.dex2jar.tools.BaksmaliBaseDexExceptionHandler.dumpZip(BaksmaliBaseDexExceptionHandler.java:135)
    at com.googlecode.dex2jar.tools.BaksmaliBaseDexExceptionHandler.dump(BaksmaliBaseDexExceptionHandler.java:92)
    at com.googlecode.dex2jar.tools.Dex2jarCmd.doCommandLine(Dex2jarCmd.java:120)
    at com.googlecode.dex2jar.tools.BaseCmd.doMain(BaseCmd.java:290)
    at com.googlecode.dex2jar.tools.Dex2jarCmd.main(Dex2jarCmd.java:33)
```

其中注意到：

* 如果报错，会有把错误信息导出到名为xxx-error.zip的压缩文件中。
  * 比如：`com.huili.readingclub2847840-error.zip`
    * 可供后续分析使用
* 后续经过确认，这些报错的，往往是没有包含app业务逻辑的，不是我们要的dex，所以可以忽略这些错误

上述所有的`dex`转换为`jar`之后：

```bash
➜  v3.4.8 ll
total 125288
-rw-------  1 crifan  staff   469K  3 21 09:55 com.huili.readingclub1166288-dex2jar.jar
-rw-r--r--  1 crifan  staff    14K  3 21 09:55 com.huili.readingclub1166288-error.zip
-rw-------  1 crifan  staff   1.1M  3 19 14:05 com.huili.readingclub1166288.dex
-rw-------  1 crifan  staff   121K  3 21 09:56 com.huili.readingclub13088280-dex2jar.jar
-rw-r--r--  1 crifan  staff    16K  3 21 09:56 com.huili.readingclub13088280-error.zip
-rw-------  1 crifan  staff    12M  3 19 14:04 com.huili.readingclub13088280.dex
-rw-------  1 crifan  staff   669K  3 21 09:56 com.huili.readingclub1461452-dex2jar.jar
-rw-r--r--  1 crifan  staff    25K  3 21 09:56 com.huili.readingclub1461452-error.zip
-rw-------  1 crifan  staff   1.4M  3 19 14:04 com.huili.readingclub1461452.dex
-rw-------  1 crifan  staff   103K  3 21 09:57 com.huili.readingclub191572-dex2jar.jar
-rw-r--r--  1 crifan  staff   7.0K  3 21 09:57 com.huili.readingclub191572-error.zip
-rw-------  1 crifan  staff   187K  3 19 14:04 com.huili.readingclub191572.dex
-rw-------  1 crifan  staff   1.6M  3 21 09:58 com.huili.readingclub2847840-dex2jar.jar
-rw-r--r--  1 crifan  staff    47K  3 21 09:58 com.huili.readingclub2847840-error.zip
-rw-------  1 crifan  staff   2.7M  3 19 14:04 com.huili.readingclub2847840.dex
-rw-------  1 crifan  staff   3.5M  3 21 09:59 com.huili.readingclub3986968-dex2jar.jar
-rw-------  1 crifan  staff   3.8M  3 19 14:04 com.huili.readingclub3986968.dex
-rw-------  1 crifan  staff   5.1M  3 21 10:00 com.huili.readingclub8725900-dex2jar.jar
-rw-r--r--  1 crifan  staff    68K  3 21 10:00 com.huili.readingclub8725900-error.zip
-rw-------  1 crifan  staff   8.3M  3 19 14:04 com.huili.readingclub8725900.dex
-rw-------  1 crifan  staff   9.5M  3 21 10:00 com.huili.readingclub8825612-dex2jar.jar
-rw-------  1 crifan  staff   8.4M  3 19 14:04 com.huili.readingclub8825612.dex
```
