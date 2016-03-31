# Write a LLVM Backend

- tags: llvm, compiler, compiler backend

------

###### 参考: [llvm官方文档](http://llvm.org/docs)

- 支持LLVM IR到V9汇编码的翻译(TargetMachine)
  - 注意
    - 需要在lib/Target/LLVMBuild.txt中添加subdirectories, 需要修改CMakeList.txt
- 需要支持inline assembly(AsmPrinter, AsmParser)
- 需要支持编译成elf文件, 并且可以使用ld链接, (MCELFObjectWriter)
- 需要支持源码级调试(elf文件中的符号信息?)
- 需要支持链接脚本(直接用llvm-ld链接?)
