# Android Decompiler

* 主页
  * [dirkvranckaert/AndroidDecompiler: Decompile any APK](https://github.com/dirkvranckaert/AndroidDecompiler)
* 功能
  * 集成了多种工具去实现反编译apk得到java代码
* 集成了哪些工具
  * `Dex2Jar`: Version 0.0.9.15
  * `android-apktool`: Version 1.5.2
  * `JD-Core-Java`: Version 1.2
  * `Artistic Style (astyle)`: Version 2.04
* 支持平台
  * Mac
  * Unix类系统
* 用法

```bash
usage: decompileAPK.sh [options] <APK-file>

options:
 -o,--output <dir>	The output directory is optional. If not set the
                         default will be used which is 'output' in the 
                         root of this tool directory.
 --skipResources	Do not decompile the resource files
 --skipJava		Do not decompile the JAVA files
 -f,--format		Will format all Java files to be easier readable. 
  			 However, use with CAUTION! This option might change 
  			 line numbers!
 -p,--project		Will generate a Gradle-based Android project for you
 -h,--help		Prints this help message

parameters:
 APK-file               A valid APK file is required as input
```
