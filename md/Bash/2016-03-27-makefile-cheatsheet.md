# Makefile cheatsheet

tags: makefile, make, autotools

------

参考: [跟我一起写Makefile](http://blog.csdn.net/haoel/article/details/2894)

1. 函数
  - 调用方法: `$(<function> <arguments)`, 参数用逗号分隔
  - 内置函数:
    - `$(subst <from>,<to>,<text>)`
      - 功能：把字串<text>中的<from>字符串替换成<to>。
      - 返回：函数返回被替换过后的字符串。
    - `$(dir <names...>)`
      - 功能：从文件名序列`<names>`中取出目录部分。目录部分是指最后一个反斜杠（“/”）之前的部分。如果没有反斜杠，那么返回“./”。
      - 返回：返回文件名序列`<names>`的目录部分。
