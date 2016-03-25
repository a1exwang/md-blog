# Vim Cheatsheet

- tags: vim, cheatsheet, vi, editor

------
#### 参考自http://vim.wikia.com/

- 多行同时改变缩进
  - `>>` 当前行向右缩进
  - '<<' 当前行向左缩进
  - 插入模式中`Ctrl-T`缩进, `Ctrl-D`返回
  - 缩进大连招
    1. 光标移到要缩进的第一行
    2. `V`, `jjjj`选择要缩进的范围
    3. `>`缩进
    4. `.`继续缩进, `u`返回
    5. `gv`恢复之前的选择范围
