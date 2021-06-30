# smali

* Smali
  * 是什么：一种`汇编语法`/`汇编文件`
    * 一种语法：`Smali语法`
      * 来源：是`Dalvik`的`VM`的字节码，即`dex`文件中的`bytecode`=`二进制数据`，反汇编后得到的：Smali代码
      * 语法：一种宽松式的Jasmin/dedexer语法
        * 它实现了`.dex`格式所有功能（注解，调试信息，线路信息等）
    * 对应文件叫：`Smali文件`
  * 举例
    * java源码：`int x = 42`
    * Dalvik编译后的，dex中`二进制数据`=`bytecode`=`字节码`：`13 00 2A 00`
      * 二进制，人类很难读懂
    * 用`baksmali`反汇编后的，smali代码：`const/16 v0, 42`
      * smali代码，人类基本可读
  * 学习Smali的用途
    * 分析Apk：静态分析，不够
      * 需要动态分析，涉及Smali
    * 修改Apk逻辑：修改Smali代码，重新编译打包Apk
      * Android逆向基础：掌握Smali
        * 能阅读 smali 代码对进行 android 逆向十分重要
  * 官网
    * JesusFreke/smali: smali/baksmali
      * https://github.com/JesusFreke/smali
* `smali`/`baksmali`
  * GitHub
    * [JesusFreke/smali: smali/baksmali](https://github.com/JesusFreke/smali)
      * smali/baksmali is an assembler/disassembler for the dex format used by dalvik, Android's Java VM implementation
  * 针对dex
    * `smali`：`assembler`=`汇编器`
      * `smali语言`=`汇编语言`
    * `baksmali`：`disassembler`=`反汇编器`
      * 安卓系统里的Java虚拟机（Dalvik）所使用的一种`.dex`格式文件的反汇编器

## Smali基本语法

* 官网文档
  * TypesMethodsAndFields · JesusFreke/smali Wiki
    * https://github.com/JesusFreke/smali/wiki/TypesMethodsAndFields


### 数据类型 Types

| Smali | Java | 备注 |
| ----- | ----- | --- |
| v | void | 只能用于返回值类型 |
| Z | boolean | |
| B | byte | |
| S | short | |
| C | char | |
| I | int | |
| J | long | |
| F | float | |
| D | double | |
| `Lpackage/name;` | 对象类型 | `L`表示这是一个对象类型，`package/name`表示该对象所在的包，`；`表示对象名称的结束<br/> `Lpackage/name/ObjectName;` 相当于`java`中的`package.name.ObjectName;`|
| `[类型` | 数组 | `[I`表示一个`int`型`数组，`[Ljava/lang/String`表示一个`String`的对象`数组` |

### 寄存器

* 官网文档
  * Registers · JesusFreke/smali Wiki
    * https://github.com/JesusFreke/smali/wiki/Registers

* Java中变量都是存放在内存中的
  * Android为了提高性能，变量都是存放在寄存器中的
    * 寄存器为32位，可以支持任何类型

* 寄存器
  * 类型
    * 本地寄存器
      * 用v开头数字结尾的符号来表示
      * 举例
        * v0, v1, v2
    * 参数寄存器
      * 用p开头数字结尾的符号来表示
      * 举例
        * p0,p1,p2
  * 注意
    * 在`非static`方法中，p0代指this，p1为方法的第一个参数
    * 在`static`方法中，p0为方法的第一个参数
  * 说明
    * 指定有多少寄存器是可用
      * `.registers`：指定了方法中寄存器的总数
      * `.locals`： 表明了方法中非参寄存器的总数，出现在方法中的第一行

#### Smali代码示例

```java
const/4 v0, 0x1 //把值0x1存到v0本地寄存器
iput-boolean v0,p0,Lcom/aaa;->IsRegisterd:Z //把v0中的值赋给com.aaa.IsRegistered，p0代表this，相当于this.Isregistered=true
```

### 成员变量？ Fields

* 格式
  ```bash
  .field public/private [static][final] varName:<类型>
  ```
* 指令
  * 获取指令
    * iget, sget, iget-boolean, sget-boolean, iget-object, sget-object
  * 操作指令
    * iput, sput, iput-boolean, sput-boolean, iput-object, sput-object
    * array的操作是aget和aput

### Smali代码示例

```java
sget-object v0,Lcom/aaa;->ID:Ljava/lang/String;
```
  * 获取ID这个String类型的成员变量并放到v0这个寄存器中

```java
iget-object v0,p0,Lcom/aaa;->view:Lcom/aaa/view;
```
  * iget-object比sget-object多一个参数p0，这个参数代表变量所在类的实例。这里p0就是this

```java
const/4 v3, 0x0
sput-object v3, Lcom/aaa;->timer:Lcom/aaa/timer;
```
* 相当于java代码
  ```java
  this.timer = null;
  ```


```java
.local v0, args:Landroid/os/Message;
const/4 v1, 0x12
iput v1,v0,Landroid/os/Message;->what:I
```
* 相当于java代码
  ```java
  args.what = 18;
  ```
    * 其中args为Message的实例


### 方法/函数 Methods

* 函数定义格式
  ```java
  .method public/private [static][final] methodName()<类型>
  .end method
  ```
* 函数类型
  * `direct method`= private方法
  * `virtual method` = 其余的方法
* 函数调用
  * 格式
```java
invoke-指令类型 {参数1, 参数2,...}, L类名;->方法名
```
  * 包含
    * invoke-direct
    * invoke-virtual
    * invoke-static
    * invoke-super
    * invoke-interface
* 函数返回结果
  * 要用指令move-result或move-result-object来保存函数返回的结果

Smali代码示例：

```java
.method private ifRegistered()Z
    .locals 2            // 本地寄存器的个数
    .prologue
    const/4 v0, 0x1      //v0赋值为1
    if-eqz v0, :cond_0   //判断v0是否等于0，等于0则跳到cond_0执行
    const/4 v1, 0x1      //符合条件分支
    :goto_0              //标签
    return v1            //返回v1的值
    :cond_0              //标签
    const/4 v1, 0x0      //cond_0分支
    goto :goto_0         //跳到goto_0执行
.end method
```

```java
const-string v0, "NDKLIB"
invoke-static {v0}, Ljava/lang/System;->loadLibrary(Ljava/lang/String;)V
```
* 相当于java代码
  ```java
  System.loadLibrary("NDKLIB")
  ```

```java
const-string v0, "Eric"
invoke-static {v0}, Lcmb/pbi;->t(Ljava/lang/String;)Ljava/lang/String;
move-result-object v2
```
* 表示将方法`t`返回的`String对象`保存到`v`2中
