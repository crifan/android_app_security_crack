# 反汇编器

在安卓安全和破解期间，可能会涉及到，底层汇编级别的反编译，会用到相关反汇编工具和框架。

此处列出一些常见的支持（安卓的arm的）`反汇编器`=`disassembler`=`反汇编框架`：

* `Capstone`
  * 最大特点：跨平台，支持多架构，包括安卓的arm
    * Capstone 支持多架构
      * Arm, Arm64 (Armv8), M68K, Mips, PowerPC, Sparc, SystemZ, TMS320C64X, XCore& X86 (incl ude X86_64)
    * 提供了多种语言的编程接口
      * Clojure, F#, Common Lisp, Visual Basic, PHP, PowerShell, Haskell, Perl, Python, Ruby, C#, NodeJS, Java, GO, C++, OCaml, Lua, Rust, Delphi, Free Pascal
  * Capstone的强大之处
    * 反汇编 + 分析
    * 编译成中间文本形式代码，便于调试
  * 主页
    * http://www.capstone-engine.org/
    * https://github.com/aquynh/capstone
  * 安装
    * Mac
      * `brew install capstone`
    * Ubuntu
      * `sudo apt-get install libcapstone3`
  * 详见
    * [安卓安全](https://book.crifan.com/books/explore_underlying_mechanism_binary_security/website/)中的[Capstone](https://book.crifan.com/books/explore_underlying_mechanism_binary_security/website/multi_plat/disassembler/capstone.html)
