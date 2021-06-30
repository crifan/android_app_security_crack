# 总结和结论

## `JD-GUI` vs `CFR` vs `Procyon` vs `Jadx` 对比总结

下面从整体总结和对比这几个反编译的反编译的效果：

| **java反编译器** | JD-GUI | CFR | Procyon | Jadx |
| ---------- | ------- | --- | ------- | ---- |
| **转换出错程度** | 比较多 | 少许 | 很少 | 极少 |
| **出错状态和相关信息** | 会显示：`/* Error */ // Byte code` | 输出转换期间出错的地方到文件：`summary.txt` | 会显示：<br/>`This method could not be decompiled.`<br/>`Original Bytecode` | |
| **转换出的代码的质量** | 不是很好，细节不够好 | 部分细节转换的略有瑕疵<br/>但是还是可以看到基本代码逻辑的 | 完美转换细节<br/>代码中字符数组定义等内容可以正确转换，但是逻辑不清晰<br/>比如只是能转换出常量解析后的字符串值，而无法识别出是常量的引用 | 不仅转换完美无错，而且代码逻辑更准确和完整<br/>代码中的常量的引用都能完美还原出来<br/>代码中字符数组定义等内容可以完美转换 |
| **转换出的文件是否有标识** | 无 | 有，顶部有标识：<br/>Decompiled with CFR 0.141<br/>并且还能列出具体出错的类：<br/>Could not load the following classes<br/> | 有，顶部有标识：<br/>Decompiled by Procyon v0.5.34 | 无 |

所以最终结论就是：

* 以后**尽量用**`Jadx`
  * 直接用jadx打开未加固的apk
    * 即可查看和导出java源代码
  * 打开（用FDex2从加固了的apk导出的）dex文件
    * 查看和导出java源代码
* 其次**考虑用**`Procyon`（或基于Procyon的GUI工具`Luyten`）
  * 查看代码：用基于Procyon的`Luyten`去查看代码
  * 导出代码：用Procyon去从jar反编译转换出java源代码
