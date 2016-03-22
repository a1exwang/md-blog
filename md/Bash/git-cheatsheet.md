# Git Cheatsheet

- tags: cheatsheet, git, version control system

------

#### Reference: Progit

## Terms

1. 工作区
2. 暂存区
3. 仓库

## Commands
- git status
  - 列出当前工作区状态
  - -s, --short
    - ?? Untracked
    -  M 在工作区修改了
    - M  在暂存区修改了
    - MM 在工作区修改了, 又在暂存区修改了
    - A  新添加到暂存区

- git add
  - 开始跟踪新文件
  - 把已跟踪的文件放到暂存区
  - 把冲突文件标记为已解决

- git diff
  - 无参数: 工作区和暂存区的变化
  - --cache/--staged: 暂存区和仓库中的区别
  - git difftool --tool=meld用meld来代替diff

- git commit
- git rm
