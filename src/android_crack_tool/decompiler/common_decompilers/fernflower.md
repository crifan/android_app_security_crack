# Fernflower

* 主页
  * 官网
    * [intellij-community/plugins/java-decompiler/engine at master · JetBrains/intellij-community](https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine)
  * 非官方 GitHub
    * [fesh0r/fernflower: Unofficial mirror of FernFlower Java decompiler (All pulls should be submitted upstream)](https://github.com/fesh0r/fernflower)
* 功能
  * Java的反编译器
    * 从Java的`class`反编译出java`源代码`
* 说明
  * IntelliJ IDEA 内置
* 用法
  * `java -jar fernflower.jar [-<option>=<value>]* [<source>]+ <destination>`
  * 举例
    * `java -jar fernflower.jar -hes=0 -hdc=0 c:\Temp\binary\ -e=c:\Java\rt.jar c:\Temp\source\`
    * `java -jar fernflower.jar -dgs=1 c:\Temp\binary\library.jar c:\Temp\binary\Boot.class c:\Temp\source\`